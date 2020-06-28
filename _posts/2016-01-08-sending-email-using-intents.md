---
layout: post
title: Sending Email using Intents
lead: Many things on Android are as easy as starting an Activity using the right Intent. Sending an email to a specific recipient is one of those things.
readtime: true
---

*This post was originally published on Medium: [Android: Sending Email using Intents](https://medium.com/@cketti/android-sending-email-using-intents-3da63662c58f#.m53umvu9z)*

Many things on Android are as easy as starting an Activity using the right Intent. Sending an email to a specific recipient is one of those things.

Sadly, there is [much](http://stackoverflow.com/questions/2197741/how-can-i-send-emails-from-my-android-application) [bad](http://www.mkyong.com/android/how-to-send-email-in-android/) [advice](http://www.tutorialspoint.com/android/android_sending_email.htm) out there on how to send emails using Intents. Because I write an open source [email app](https://github.com/k9mail/k-9) I have a pretty good understanding of what goes on behind the scenes. That’s why I believe I know better than all those other people :)


## ACTION_SENDTO
To start the Activity to compose an email in your user’s favorite email app you use an Intent with the [`ACTION_SENDTO`](https://developer.android.com/reference/android/content/Intent.html#ACTION_SENDTO) action. Unfortunately, the documentation is very sparse. It simply states:

> **Activity Action:** Send a message to someone specified by the data.  
> **Input:** getData() is URI describing the target.  
> **Output:** nothing.  

This doesn’t mention email at all because `ACTION_SENDTO` is very generic and can also be used to send e.g. SMS, MMS or XMPP messages.
To send an email we have to use a *mailto* URI as defined by [RFC 6068](https://tools.ietf.org/html/rfc6068). In its simplest form such a URI consists of `mailto:` followed by an email address, e.g. `mailto:alice@example.org`. You might recognize this syntax from email links in HTML documents.

Creating such an Intent might look like this:

<script src="https://gist.github.com/cketti/51938e906959e66d7d6d.js"></script>

Most of the time you want to provide more data than just a recipient. And the *mailto* specification allows us to also specify CC and BCC recipients, a subject, and even text for the email body.

    mailto:bob@example.org?cc=alice@example.com&subject=Important%20message&body=Hi%20there

Generating such a *mailto* URI is a bit tedious because you have to [percent-encode](https://tools.ietf.org/html/rfc3986#section-2.1) certain characters as you can see in the example above.
Android’s [`Uri.Builder`](https://developer.android.com/reference/android/net/Uri.Builder.html) class would be the perfect fit since it makes it easy to add query parameters while taking care of the encoding. Unfortunately, building Uri instances doesn’t work very well for non-hierarchical URIs like *mailto* URIs. One way to work around that is to manually construct the URI and dealing with the encoding.

<script src="https://gist.github.com/cketti/6a9b67dd92540bc74b2e.js"></script>

[Some](http://stackoverflow.com/a/9462834/1800174) [code](http://stackoverflow.com/a/15022153/1800174) [samples](http://developer.android.com/guide/components/intents-common.html#Email) advocate the use of [`EXTRA_SUBJECT`](https://developer.android.com/reference/android/content/Intent.html#EXTRA_SUBJECT), [`EXTRA_TEXT`](https://developer.android.com/reference/android/content/Intent.html#EXTRA_TEXT), etc. Those are certainly easier to use. However, the Android API reference only mentions them in connection with [`ACTION_SEND`](https://developer.android.com/reference/android/content/Intent.html#ACTION_SEND) and [`ACTION_SEND_MULTIPLE`](https://developer.android.com/reference/android/content/Intent.html#ACTION_SEND_MULTIPLE). Those are more general Intents for sharing content to nobody in particular.
The fact that the Extras also work with `ACTION_SENDTO` was an undocumented “feature” of AOSP Email and the Gmail app. That functionality then had to be copied by all other Android email clients because apps were and are using those Extras.
But since all major email clients [support](https://github.com/cketti/EmailIntentBuilder/wiki/EmailClientCompatibilityList) the use of query parameters in *mailto* URIs I see no reason to use an undocumented feature and advice against it.

It is also worth mentioning that you shouldn’t use [`Intent.createChooser()`](https://developer.android.com/reference/android/content/Intent.html#createChooser%28android.content.Intent,%20java.lang.CharSequence%29) to launch an email Intent. Users most likely have a preferred email app that they want to be able to select as default app. The standard behavior when resolving an Intent deals with that just fine.

{: .image-in-post}
![Screenshot of chooser dialog](/img/sending-email-using-intents/screenshot_chooser.png)  
Allow users to select a default app

There are a couple of other things that need to be considered. Line breaks in the body, for example, need to be encoded as `%0D%0A` (CRLF).
Because it’s no fun to deal with all of that when all you want to do is send an email, I wrote a small library to take care of the dirty details for you.


## EmailIntentBuilder — Making life easier

The goal of the Email Intent Builder library is to make creating email Intents as easy as possible.
You can find it on [Maven Central](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22de.cketti.mailto%22%20AND%20a%3A%22email-intent-builder%22), the [source code](https://github.com/cketti/EmailIntentBuilder) on GitHub.

Building an email Intent is a simple matter of calling some methods on the builder:

<script src="https://gist.github.com/cketti/f4161c07ea9b7ae66f0d.js"></script>

Most of the time you also want to launch the Intent. The `start()` method will do that for you while also taking care of not throwing an exception if no app could be found to handle the Intent.

<script src="https://gist.github.com/cketti/988ff9de4b8460a9232d.js"></script>


## What about Attachments?

Unfortunately, the `ACTION_SENDTO` Intent doesn’t support attachments. If you need to send an email containing one or more attachments you should use Android’s more generic share mechanism, i.e. `ACTION_SEND` or `ACTION_SEND_MULTIPLE`.
A lot of people have realized that this leads to quite a few more than just email apps showing up in the app chooser dialog. How to properly deal with that is material for another post.


---

I’d love to hear about your experiences dealing with email on Android. Let me know on [Twitter](https://twitter.com/cketti).
