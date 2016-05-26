---
layout: page
title: Projects
subtitle: Software I work on in my free time
---

# Apps
Most of the time I'm working on K-9 Mail. But occasionally I find the time to create a small app.


### K-9 Mail
This is what got me into Android development. **K-9 Mail** is a powerful email client for Android that is currently used by more than 2 million people. And it's probably one of the oldest open source Android apps.

To date over [140 people](https://github.com/k9mail/k-9/graphs/contributors) have contributed to the app. But there is still a lot of work to be done. And we welcome every helping hand. Head over to the [project page](https://github.com/k9mail/k-9) on GitHub to learn more.

![Screenshot](/img/k9mail.png)

You can download [K-9 Mail](https://play.google.com/store/apps/details?id=com.fsck.k9) from Google Play. The [source code](https://github.com/k9mail/k-9) is available on GitHub.


### Attach Contact
This app allows you to attach contacts to your emails just like any other file. Android's *Contacts* app itself only supports this functionality via the *Share* action. But that can't be used e.g. when replying to an email.

[Attach Contact](https://play.google.com/store/apps/details?id=de.cketti.attachcontact) is available on Google Play.


### K-9 Mail DashClock Extension
This is an extension for the popular DashClock Widget to display the number of unread messages in K-9 Mail.

![Screenshot](/img/k9mail_for_dashclock.png)

You can download [K-9 Mail DashClock Extension](https://play.google.com/store/apps/details?id=de.cketti.dashclock.k9) from Google Play. The [source code](https://github.com/cketti/DashClock_K-9) is available on GitHub.

### K-9 Mail for SmartWatch
If you own a Sony SmartWatch 2 and use K-9 Mail on your phone you might be interested in this app. It displays notifications for new mails on the smartwatch.

![Screenshot](/img/k9mail_for_smartwatch.png)

You can download [K-9 Mail for SmartWatch](https://play.google.com/store/apps/details?id=de.cketti.smartwatch.k9) from Google Play. The [source code](https://github.com/cketti/SmartK9) is available on GitHub.


# Libraries
I created a couple of small libraries that aim to make developers' lives easier. They have all been released under an open source licence and are available on Github.

### ckChangeLog
[ckChangeLog](https://github.com/cketti/ckChangeLog) provides an easy way to display a change log in your Android app.  
It uses a simple XML file as data source and supports translations using Android's resource system.

![Screenshot](https://github.com/cketti/ckChangeLog/raw/master/screenshot_1.png)

### SafeContentResolver
[SafeContentResolver](https://github.com/cketti/SafeContentResolver) is a replacement for Android's ContentResolver that protects against the [Surreptitious Sharing](https://www.ibr.cs.tu-bs.de/news/ibr/surreptitious-sharing-2016-04-04.xml) attack.

### EmailIntentBuilder
[EmailIntentBuilder](https://github.com/cketti/EmailIntentBuilder) is an Android library for the creation of a `android.intent.action.SENDTO` Intent with a `mailto:` URI. Apps can use this Intent to tell the user's email app to compose a new message with some fields prepopulated.

Example usage:
{% highlight java %}
EmailIntentBuilder.from(activity)
        .to("alice@example.org")
        .cc("bob@example.org")
        .bcc("charles@example.org")
        .subject("Message from an app")
        .body("Some text here")
        .start();
{% endhighlight %}
