---
layout: post
title: My first year as a full-time open source developer
lead: "Looking back on the open source work I did in 2020."
tags: ["opensource", "year-in-review"]
readtime: true
---
Pandemic aside, 2020 has been an exciting year for me.

For more than 10 years I was working on open source software in my spare time. Then, in late 2019, a grant from the 
[Prototype Fund](https://prototypefund.de/) allowed me to work on [K-9 Mail](https://k9mail.app/) full-time for six months.
And it was awesome! So afterwards I decided to just keep going. I was working as a freelancer, so there
wasn't really a job I had to quit first.

Here's a probably incomplete list of open source-y things I did in 2020. It's also rather brief because
I still haven't figured out how to write blog posts without rewriting most of it, then rewriting it some more, and then
throwing away half of it because I don't like those parts anymore.  
It feels like I'm slowly getting better, though 🤞


## K-9 Mail

I've spent most of my time working on K-9 Mail. The app was in a 
[difficult state](https://k9mail.app/2020/06/01/Whats-Up-With-K-9-Mail). The last stable release was in
September 2018. My goal was to publish a new stable version in 2020. By releasing 22 beta versions we got closer to that
goal. But the app is still not in a state where I'm comfortable cutting a new stable release 😞

As K-9 Mail's maintainer I'm also dealing with all the non-development-related aspects of the project:
- In 2020 the website got a new domain name – [k9mail.app](https://k9mail.app) – and a redesign, thanks to 
  [Anxhelo Lushka](https://github.com/AnXh3L0). 
- I set up a [discourse](https://www.discourse.org/) instance to replace the mailing list: [forum.k9mail.app](https://forum.k9mail.app/)
- And the project now has a presence on Twitter ([@k9mail_app](https://twitter.com/k9mail_app)) and 
  Mastodon ([@k9mail@fosstodon.org](https://fosstodon.org/@k9mail)).


## Jitsi Hacks

Due to the pandemic much of my social life took place in video conferences, powered by the wonderful open source project 
[Jitsi](https://jitsi.org/). At some point I started poking around in the browser's developer tools trying to do things
the web interface wasn't built to do. This resulted in multiple "hacks" that I shared with friends.

Since by then I had convinced myself that I was an "open source developer" I figured I should publish this little side
project. So I created a small website containing "installation" and usage instructions for the different "hacks".  
I am quite proud of myself because I refrained from buying a domain for the project. A sub-domain does just fine for a
small side project: [jitsi-hacks.cketti.eu](https://jitsi-hacks.cketti.eu/)


## Blog posts

In 2020 I published five blog posts. That is five more than the year prior 😀

- [content:// URIs and OkHttp](https://cketti.de/2020/05/23/content-uris-and-okhttp/)
- [What's up with K-9 Mail?](https://k9mail.app/2020/06/01/Whats-Up-With-K-9-Mail)
- [android.net.MailTo is broken](https://cketti.de/2020/06/22/android-net-mailto-is-broken/)
- [Why I hide GitHub issue comments](https://cketti.de/2020/07/07/why-i-hide-github-issue-comments/)
- [Avoid Intent.resolveActivity()](https://cketti.de/2020/09/03/avoid-intent-resolveactivity/)


## Contributions to open source projects

In 2020 I contributed to quite the variety of open source projects.

### Own projects

Aside from the ones previously mentioned I also worked on these projects of mine:
- [MailToCompat](https://github.com/cketti/MailToCompat) - because Android's `MailTo` class is [broken](https://cketti.de/2020/06/22/android-net-mailto-is-broken/) I created a fixed version
- [SafeContentResolver](https://github.com/cketti/SafeContentResolver) - after existing for 4 years as version 0.9.0 without any issues I figured it was time to promote the library to version 1.0.0
- [smartwatch2048](https://github.com/cketti/smartwatch2048) - open sourced an old and abandoned project

### Other projects
- [android/storage-samples](https://github.com/android/storage-samples/pull/55) - corrected some inaccuracies in code/comments related to Android's URI permissions 🧐
- [AndroidStudyGroup/conferences](https://github.com/AndroidStudyGroup/conferences/pulls?q=is%3Apr+author%3Acketti+created%3A2020) - added some conferences, improved the CI workflow, and cleaned up the generated HTML/JavaScript
- [androidx](https://github.com/androidx/androidx/commits?author=cketti&since=2020-01-01&until=2020-12-31) - fixed a memory leak, fixed the `MailTo` class, fixed `ShareCompat.IntentBuilder` 🐛
- [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll/pulls?q=is%3Apr+author%3Acketti+created%3A2020) - various minor improvements I wanted to use on cketti.de
- [bulma-clean-theme](https://github.com/chrisrhymes/bulma-clean-theme/pull/75) - very minor fix to the generated HTML
- [c-calendar](https://github.com/c-base/c-calendar/pulls?q=is%3Apr+author%3Acketti+created%3A2020) - improved the [c-base calendar](https://www.c-base.org/calendar) page
- [dbbahnhoflive-android](https://github.com/dbbahnhoflive/dbbahnhoflive-android/pull/3) - some minor fixes; apparently the first community contribution 🥇
- [discourse](https://github.com/discourse/discourse/pull/9740) - fixed a bug in the quick start guide I noticed when setting up K-9 Mail's new forum
- [EventFahrplan](https://github.com/EventFahrplan/EventFahrplan/pulls?q=is%3Apr+author%3Acketti+created%3A2020) - various fixes and refactorings
- [FairEmail](https://github.com/M66B/FairEmail/pull/187) - replaced usage of the `MailTo` class with the one from the AndroidX Core library
- [gstreamer/gst-plugins-bad](https://gitlab.freedesktop.org/gstreamer/gst-plugins-bad/-/merge_requests/1317) - make `curlsmtpsink` use a less wrong date format when generating emails
- [iNPUTmice/jmap](https://github.com/iNPUTmice/jmap/pulls?q=is%3Apr+author%3Acketti+created%3A2020) - various fixes and small improvements
- [jakewharton.com](https://github.com/JakeWharton/jakewharton.com/pull/23) - fixed number format in a blog post; apparently the first real external contribution 🎉
- [jitsi/handbook](https://github.com/jitsi/handbook/pull/121) - small improvements to the documentation on how to build Jitsi Meet from source
- [kotlin](https://github.com/JetBrains/kotlin/pulls?q=is%3Apr+author%3Acketti+created%3A2020) - fixes to the parameter popup; [tweet including video](https://twitter.com/cketti/status/1303019601547145216) 🎥
- [leakcanary](https://github.com/square/leakcanary/pull/1806) - make it harder to accidentally include LeakCanary in release builds
- [moshi-gson-interop](https://github.com/slackhq/moshi-gson-interop/pulls?q=is%3Apr+author%3Acketti+created%3A2020) - small documentation fixes
- [okhttp](https://github.com/square/okhttp/pull/6164) - fixed code to read length of [DER-encoded](https://en.wikipedia.org/wiki/X.690#DER_encoding) values
- [TokenAutoComplete](https://github.com/splitwise/TokenAutoComplete/pulls?q=is%3Apr+author%3Acketti+created%3A2020) - small fixes/improvements needed for K-9 Mail


## Donations to open source projects

I usually use the [I love Free Software Day](https://fsfe.org/activities/ilovefs/2020/index.en.html) as a reminder to
financially support the open source projects that are important to me. In 2020 I gave money to the following projects:
- [andOTP](https://github.com/andOTP/andOTP)
- [Dino](https://dino.im/)
- [Fosstodon](https://fosstodon.org/)
- [KeePassXC](https://keepassxc.org/)
- [Let's Encrypt](https://letsencrypt.org/)
- [Liberapay](https://liberapay.com/)
- [lichess.org](https://lichess.org/)
- [Matrix](https://matrix.org/)
- [Signal](https://signal.org/)
- *The Great Suspender* - Sadly, the software seems to have changed owners since then. And the extension [might contain malware now](https://www.theregister.com/2021/01/07/great_suspender_malware/) 😞
- [Thunderbird](https://www.thunderbird.net/)
- [Tusky](https://tusky.app/)
- [Ubuntu](https://ubuntu.com/)

I also sponsored the following individuals via GitHub sponsors:
- [chrisrhymes](https://github.com/chrisrhymes) - creator of the [bulma-clean-theme](https://github.com/chrisrhymes/bulma-clean-theme) Jekyll theme I used for the Jitsi Hacks website
- [johnjohndoe](https://github.com/johnjohndoe) - maintainer of the [EventFahrplan](https://github.com/EventFahrplan/EventFahrplan) Android app
- [mikepenz](https://github.com/mikepenz) - creator of the [MaterialDrawer](https://github.com/mikepenz/MaterialDrawer) and [FastAdapter](https://github.com/mikepenz/FastAdapter) libraries we use in K-9 Mail

I do most of my development work in [IntelliJ IDEA](https://www.jetbrains.com/idea/)-based IDEs. The open source 
applications IntelliJ IDEA Community Edition and Android Studio provide all the functionality I need. But to do my part
in ensuring the company behind IntelliJ IDEA and the creators of the 
[Kotlin programming language](https://kotlinlang.org/) stick around, I purchased a license for IntelliJ IDEA Ultimate
edition.


## Financials

Most of my income in 2020 came from the Prototype Fund project. But some of it came from people who donated money using
one of these platforms:

### GitHub Sponsors

I signed up to the GitHub sponsors program as soon as I heard about it. On my [sponsors page](https://github.com/sponsors/cketti)
users could select one of the following tiers: $1 a month, $5 a month, $25 a month, $1000 a month. There are no rewards
associated with any of the tiers.  
To no one's surprise, nobody signed up for the $1000 tier. But people did sign up for all of the other tiers. In total I had 29 sponsors.
Some of them canceled their sponsorship after a month or two, but most of them kept it going ❤️  
The total payout was **966.82 EUR**. Some of that was from GitHub matching contributions. But, honestly, I can't
tell if there's a system when GitHub is matching contributions and when they're not.

### Liberapay

In 2020 [K-9 Mail's Liberapay account](https://liberapay.com/k9mail) received **4,794.91 EUR** from ~250 patrons. That 
is more than double the amount received in 2019 📈

### Total

That's a total of **5,761.73 EUR** in donations. Not bad. But certainly not enough to live on in Germany. It looks like
someone  needs to come up with a better plan for 2021 😀


## Conclusion

I was disappointed with how my first year as a full-time open source developer went. I didn't accomplish the one goal I
had: releasing a new stable version of K-9 Mail.  

But writing this blog post made me feel better. It made me realize that small contributions add up to quite a bit. 
Another way to see that is by comparing my GitHub contribution graphs for 2019 and 2020.

![GitHub contributions in 2019](/img/my-first-year-as-a-full-time-open-source-developer/github_contributions_2019.png)

![GitHub contributions in 2020](/img/my-first-year-as-a-full-time-open-source-developer/github_contributions_2020.png)

During the past 8 years I haven't done much web development. Working on Jitsi Hacks made me realize that I still enjoy
it quite a bit. I'll probably end up doing more of that in the future.


## Plans for 2021

I have quite a few ideas I want to work on this year. But my most important goals remain the same as they were in 2020:
- Finally release a new stable version of K-9 Mail.
- Figure out how to be a full-time open source developer without using up all of my savings.


## Thanks

My thanks goes to everyone who has contributed to one of my projects, to the people who reviewed my blog posts, and
to everyone who has helped me stay sane this last year.  
A special thanks goes to all of the sponsors who have made this journey possible ❤️
