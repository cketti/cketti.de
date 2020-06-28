---
layout: post
title: "android.net.MailTo is broken"
lead: "How broken exactly? Can anything be done about it? And what's this for anyway? All questions that will be answered in this post."
tags: ["android", "email"]
readtime: true
cover-img: /img/android-net-mailto-is-broken/broken.jpg
share-img: /img/android-net-mailto-is-broken/broken.jpg
---

The [MailTo](https://developer.android.com/reference/android/net/MailTo) class has been part of the Android Platform API from the very start.
And the class hasn't been changed in a significant way since then. This could mean the API is very good and the code doesn't contain any known bugs.
Sadly, that's not the case. `android.net.MailTo` is broken and shouldn't be used. Let's find out what's wrong exactly.

But I'm guessing most Android developers have never heard of this class before. So, first, let's have a quick look at the documentation for `MailTo` to find out what it is about.

> This class parses a mailto scheme URL and then can be queried for the parsed parameters. This implements RFC 2368.

And here's a quick example of how the class is used:

```java
MailTo mailToUri = MailTo.parse(
    "mailto:recipient@domain.example?subject=Hello%20World&body=Hi");

String recipient = mailToUri.getTo();    // recipient@domain.example
String subject = mailToUri.getSubject(); // Hello World
String body = mailToUri.getBody();       // Hi
```

## What is broken exactly?

The bugs are in [`MailTo.parse()`](https://android.googlesource.com/platform/frameworks/base/+/6090995951c6e2e4dcf38102f01793f8a94166e1/core/java/android/net/MailTo.java#64). Let's look at them one by one.

### Use of Uri.parse()

After making sure the supplied `url` starts with `mailto:`, `Uri.parse()` is invoked to parse the remainder of the `url` string.

```java
// Strip the scheme as the Uri parser can't cope with it.
String noScheme = url.substring(MAILTO_SCHEME.length());
Uri email = Uri.parse(noScheme);
// …
String address = email.getPath();
```

So if the input to `MailTo.parse()` was `mailto:alice@domain.example?subject=Hello`, `Uri.parse("alice@domain.example?subject=Hello")` is called.

Now you might be asking yourself two things:

1. Why is the `mailto:` prefix removed before passing the URL to `Uri.parse()`?
2. Why doesn't `Uri.parse()` complain that the input is missing a scheme identifier?

The answer to the first question is that many `Uri` methods only work for hierarchical URIs. Those are URIs where the scheme identifier is followed by `://`, e.g. `https://authority/path?query#fragment`. If the `MailTo` class were using `Uri.parse("mailto:alice@domain.example?subject=Hello")` there would be no way to extract `alice@domain.example` using one of `Uri`'s methods.

Reading the documentation (or source code) of the `Uri` class reveals the answer to the second question. The `Uri` class also supports relative URIs, i.e. ones without a scheme identifier. These are automatically treated as hierarchical URIs. And that's why `email.getPath()` returns the recipient address `alice@domain.example`.

Wanting the input to be parsed as relative URL is the source of the first bug. If one of the query parameters contains an unencoded `:` character, the input won't be treated as a relative URL. Instead everything up to the colon will be treated as scheme identifier.

Example:
```java
Uri parsed = Uri.parse("alice@domain.example?body=oh:no");

String scheme = parsed.getScheme();                     
// Result: alice@domain.example?body=oh

String schemeSpecific = parsed.getSchemeSpecificPart();
// Result: no
```

To be fair, [RFC 2368](https://tools.ietf.org/html/rfc2368) requires all URL reserved characters (and that includes `:`) in a header value to be percent-encoded (`%3A`). So an RFC 2368-compliant URL should look like this: `mailto:alice@domain.example?body=oh%3Ano`.
However, this restriction has been relaxed in [RFC 6068](https://tools.ietf.org/html/rfc6068) which replaced RFC 2368 in 2010. Now the colon and some other characters are allowed to be used without encoding inside header field values. This also frequently happens in real world scenarios.
The result is that `mailto` URIs containing an unencoded `:` are not parsed properly by the `MailTo` class. And this is not limited to the header field containing the colon. None of the URI is parsed correctly.


### Use of Uri.getQuery()

The next issue is the use of `Uri.getQuery()`.

```java
// Parse out the query parameters
String query = email.getQuery();
if (query != null ) {
  String[] queries = query.split("&");
  for (String q : queries) {
    String[] nameval = q.split("=");
    if (nameval.length == 0) {
        continue;
    }
    // insert the headers with the name in lowercase so that
    // we can easily find common headers
    m.mHeaders.put(Uri.decode(nameval[0]).toLowerCase(Locale.ROOT),
        nameval.length > 1 ? Uri.decode(nameval[1]) : null);
  }
}
```

`Uri.getQuery()` returns the query part of the URI with percent-encoded characters decoded. So with `mailto:?body=Q%26A%3Dnice&subject=Hi` as input we end up with `body=Q&A=nice&subject=Hi` in the variable `query`. Reading a bit further in the code snippet we can see how this becomes a problem when the string is split on the `&` character. We end up with an array containing the elements `body=Q`, `A=nice`, `subject=Hi`, breaking the body text apart. The mistake is that `Uri.getQuery()` was used instead of `Uri.getEncodedQuery()` to get the encoded query.


### Double decoding

After extracting the query parameters `Uri.decode()` is used to percent-decode the individual strings. But since `Uri.getQuery()` already decoded the query once, we now end up with double decoding. For example, the body value in `mailto:?body=%2525` is first decoded to `%25`, then again to `%`.
This double decoding bug is only a side-effect of the previous bug. Once that one is fixed, the code that is decoding the query actually produces the expected result.


## We should get the class fixed, right?

Over the years these bugs have been reported numerous times via Android's issue tracker. They have either been closed during an issue tracker cleanup or closed because the issue wasn't understood properly. I have created a new [issue](https://issuetracker.google.com/issues/153161703) that includes a link to my [MailToBugs repository](https://github.com/cketti/MailToBugs) which contains failing tests for all of these bugs.  
But even with a fix in a new Android version, apps would still need to work around the bugs as long as they want to support older platform versions. And we all know it would probably be 5+ years before we could drop the workarounds. 😞

### Fixed version

If you are using the platform's `MailTo` class and are looking for a drop-in replacement without these bugs, check out my [`MailToCompat`](https://github.com/cketti/MailToCompat) library: [https://github.com/cketti/MailToCompat](https://github.com/cketti/MailToCompat).


## Should I be using `MailTo`?

Unless you're writing an email client, probably not. Yet, I've seen lots of snippets that try to handle clicks on `mailto` URIs in a `WebView`. They look something like this:

```java
// DON'T DO THIS
public class MyWebViewClient extends WebViewClient {
  // …

  @Override
  public boolean shouldOverrideUrlLoading(WebView view, String url) {
    Uri uri = Uri.parse(url);

    if (uri.getScheme().equalsIgnoreCase("mailto")) {
      MailTo mailTo = MailTo.parse(url);

      // DON'T DO THIS
      Intent intent = new Intent(Intent.ACTION_SEND);
      intent.setType("message/rfc822");
      intent.putExtra(Intent.EXTRA_EMAIL, new String[] { mailTo.getTo() });
      intent.putExtra(Intent.EXTRA_TEXT, mailTo.getBody());
      intent.putExtra(Intent.EXTRA_SUBJECT, mailTo.getSubject());
      intent.putExtra(Intent.EXTRA_CC, mailTo.getCc());

      context.startActivity(intent);
      return true;
    }

    // …
  }
}
```

That's unnecessary. Email apps handle `mailto:` URIs just fine. `WebView`'s default behavior of using `ACTION_VIEW` with the URI works just fine.
Alternatively, you could use `ACTION_SENDTO` with the unmodified URI. For more information check out my blog post [Sending Email using Intents](https://cketti.de/2016/01/08/sending-email-using-intents/).


## Summary

The fact that `android.net.MailTo` hasn't been fixed in all those years is a good indicator that the class isn't widely used. The main audience is authors of email clients. And we all had to either learn the hard way that we can't rely on this class or never heard about it and went with our own implementation right from the start. As far as I can tell nowadays almost nobody is using `android.net.MailTo`. So let's just mark it as `@Deprecated` and forget all about it. ⚰️


Photo by [Ruben Mishchuk](https://unsplash.com/@ruben244?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText) on [Unsplash](https://unsplash.com/photos/EC5AQfxgxdE)
