---
layout: post
title: Share URL to Clipboard
---

On Android many apps allow the user to share the currently displayed content to another app. Often it's a link to the content on the web together with some additional information, e.g. the headline and maybe the lead of a news article.


## Share to clipboard

A couple of weeks back I saw the following tweet in my timeline.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">
Hey native apps: if I share to clipboard, just give me the URL, not the URL &amp; &quot;hey kids check out this cool
link&quot; or some other bullshit</p>
&mdash; Jake Archibald (@jaffathecake)
<a href="https://twitter.com/jaffathecake/status/726815002724847617">May 1, 2016</a>
</blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Judging by the reactions, Jake is not the only one frustrated by this. So let's have a closer look at how sharing to the clipboard works and how the requested feature can be implemented.


## Sharing text on Android

Sharing content on Android is as simple as creating an Intent with the [`ACTION_SEND`](https://developer.android.com/reference/android/content/Intent.html#ACTION_SEND) action. You also have to specify the media type of the content. In this case we're only interested in text, so the type is `text/plain` and the content itself goes into the [`EXTRA_TEXT`](https://developer.android.com/reference/android/content/Intent.html#EXTRA_TEXT) extra.

{% highlight java %}
Intent shareIntent = new Intent();
shareIntent.setAction(Intent.ACTION_SEND);
shareIntent.setType("text/plain");
shareIntent.putExtra(Intent.EXTRA_TEXT, "hey kids check out this cool link\n" +
        "https://example.org/cool-link");

startActivity(Intent.createChooser(shareIntent, "Share with"));
{% endhighlight %}

And that's about all app developers have to do in order to show the Share dialog.


## Copy to Clipboard

As you can see in the image below *"Copy to clipboard"* is an option in the list of available Share targets.

{: .image-in-post}
![Share dialog](/img/share-url-to-clipboard/screenshot_share.png)

What many people probably don't know is that this is not a feature built into the Android platform. The *Copy to clipboard* action is [part of the Google Drive app](http://www.androidpolice.com/2012/11/29/tip-drives-latest-update-adds-global-copy-to-clipboard-option-in-the-share-menu/) and was only added at the end of 2012.

And of course there exist [many](https://play.google.com/store/search?q=copy%20to%20clipboard) [more](https://f-droid.org/repository/browse/?fdfilter=copy+to+clipboard) applications that provide the same functionality. So the easiest solution, sharing only the URL when the user selects *Copy to clipboard*, is not really feasible.


## Option 1: Only share the link

The simplest way to satisfy the original request is to put only the URL into `EXTRA_TEXT` extra of the Share Intent.

This way only the URL ends up in the clipboard when *Copy to Clipboard* is selected. But let's say you want to send a link to a news article to a friend. In that case the headline and a short excerpt would surely be much appreciated by the recipient. And that's the reason why most apps provide this additional text.


## Option 2: Don't share

A possible way around this situation is to not use the Share facility and instead provide another way to copy a link to the clipboard. Twitter, for example, added a *"Copy link to Tweet"* entry to its menu.

{: .image-in-post}
![Twitter menu](/img/share-url-to-clipboard/screenshot_twitter_menu.png)

Functionality-wise this should make most users happy. Getting only the link is easy enough, while sharing uses additional text to provide some context.

However, this can lead to a confusing user experience. By now users know that *Copy to Clipboard* can be found in the Share dialog and [don't necessarily look elsewhere](https://twitter.com/DasSurma/status/726815207918587908).


## Option 3: Extend the Share dialog

Fortunately, it's easy enough to add your own action to the Share dialog. So let's add a *Copy link to clipboard* entry that does just that. While all regular Share targets receive the link and additional text.

To make this work, we slightly modify the Share snippet from before.

<script src="https://gist.github.com/cketti/bf1f44cd21beb5061b772be339fd7fa7.js"></script>

Using [`EXTRA_INITIAL_INTENTS`](https://developer.android.com/reference/android/content/Intent.html#EXTRA_INITIAL_INTENTS) we can pass in a list of Intents that will be added to the Chooser dialog. In this case we point to an the Activity `CopyToClipboardActivity` that we still need to define.

<script src="https://gist.github.com/cketti/77a3ca308c7528f3fa6febeeedaa0fd0.js"></script>

In `onCreate()` we simply get the URL from the Intent that started the Activity and copy it to the clipboard. Then we finish the Activity right away to return to the screen where the Share event originated.

The icon and label we give `CopyToClipboardActivity` in the app manifest are the ones being used by the Chooser dialog when displaying our custom entry.
Using the transparent theme disables the activity transition animation when our short-lived Activity is launched.

<script src="https://gist.github.com/cketti/1ea1b31fa3e75046ec0db2fdbc04f06e.js"></script>

And here is what it looks like to the user:

{: .image-in-post}
![Share dialog with 'Copy link to clipboard' option](/img/share-url-to-clipboard/screenshot_share_with_copy_link.png)

Of course there's still the "Copy to clipboard" provided by the Drive app. And it stills copies all of the text to the clipboard. Maybe sometimes this is just what your users want. For all the other times, when it's just the URL they're after, the *Copy link to clipboard* option is right there at the top.

The source code of a [sample application](https://github.com/cketti/ShareUrlToClipboard) demonstrating all of this can be found on GitHub.


## I'm lazy. Any other option?

As a developer, you, of course, created an app that is a shining example when it comes to copying links. But what about the other apps you use? Their creators are busy implementing all of your other feature requests. Now what?

Fortunately, Android's powerful Intent mechanism means you don't actually need the cooperation of app authors to get the desired functionality. All you need is [an app](https://play.google.com/store/apps/details?id=nl.robwu.copylink) that hooks into the Share dialog and then extracts links from the text shared to it.
Writing such an app is easy enough and will be the topic of a future post.

If you have other ideas on how to make copying links to the clipboard easier, I'd love to hear from you. I'm [@cketti](https://twitter.com/cketti) on Twitter.
