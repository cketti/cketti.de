---
layout: post
title: My second year as a full-time open source developer
lead: "An overview of my open source activities and financials in 2021."
tags: ["opensource", "year-in-review"]
readtime: true
---

2020 was [my first year as a full-time open source developer](https://cketti.de/2021/01/14/my-first-year-as-a-full-time-open-source-developer/). Writing about it in this blog was a nice way to reflect on the year. And some people seemed to have enjoyed it.

So here's a summary of how my 2021 went.


## K-9 Mail

Most of my "open source time" is spent on [K-9 Mail](https://github.com/k9mail/k-9). I first started contributing to the project in 2010 and became the project lead in 2014.  
The reason I decided to dedicate all of my time to open source is because I wanted to spend more time working on K-9 Mail. There's certainly enough issues in the bug tracker to keep me busy for a couple of years.

The goal for 2020 was to release a new version of the app (the last stable version was from September 2018). If you've read my blog post reviewing that year, you know that I didn't manage to accomplish that goal. But I'm happy to report that 2021 was the year that finally saw the release of a new stable version - [K-9 Mail 5.800](https://k9mail.app/2021/07/24/K-9-Mail-is-back).

Even though it took a very long time to get that version done, it was far from perfect. When we built up the new user interface, not all features of the old UI made it into the new version right away. It was always the goal to re-implement those features. But development dragged on. So at some point I decided it was more important to release a new version than it was to get to feature parity.  
Of course, not all users agreed. Some hated the new user interface. Some really missed the features that didn't make the cut. Some shared their opinions on how to run an open source project 🙄 But there were also a lot of users who liked the new look.

[Work](https://github.com/k9mail/k-9/milestone/28) on the [next release](https://forum.k9mail.app/t/plans-for-k-9-mail-6-000/2936) is ongoing, but somewhat slow. It doesn't help that some device vendors decided their Android version will do things differently for no good reason 😭

Read more on what the project has been up to in [2021 in Review](https://k9mail.app/2022/01/18/2021-in-Review).


## Blog posts

cketti from last year believed he was getting better at writing blog posts. It looks like his assessment has not been entirely accurate.

The only post I published in 2021 was a list of things I did the year before that 😐

- [My first year as a full-time open source developer](https://cketti.de/2021/01/14/my-first-year-as-a-full-time-open-source-developer/)


## Contributions to open source projects

Even though I spent almost all of my time working on K-9 Mail, I still managed to make a couple of small contributions to other open source projects.

### Own projects

- [AdbScreenAwake](https://github.com/cketti/AdbScreenAwake) - Inspired by [@ErikHellman](https://twitter.com/ErikHellman) complaining that there should be an Android developer option called "Keep screen on while ADB is connected", I hacked up a quick prototype app to do just that. You can read a bit more about it in this [Twitter thread](https://twitter.com/cketti/status/1454129384017866755).
- [Jitsi Hacks](https://github.com/cketti/jitsi-hacks) - I updated some of the hacks to make them work with newer versions of Jitsi Meet. (Un)fortunately, the Jitsi team is evolving Jitsi Meet at an incredible pace. Whenever they change the user interface, there's a good chance some of the hacks will stop working 😢
- [MailToCompat](https://github.com/cketti/MailToCompat) - I deprecated the library because the functionality is now available as [androidx.core.net.MailTo](https://developer.android.com/reference/kotlin/androidx/core/net/MailTo). Check out the blog post [android.net.MailTo is broken](https://cketti.de/2020/06/22/android-net-mailto-is-broken/) for more details.
- [The Great Suspender (fork)](https://github.com/cketti/thegreatsuspender) - After the extension in the Chrome Web Store was suspected to contain malware, I forked the repository to build my own version with all of the "phone home" functionality removed.  
Please note that I have no intention of maintaining this extension for anyone but myself. Feel free to use it. But don't tell me about it if it doesn't work for you 😜

### Other projects
- [AndroidStudyGroup/conferences](https://github.com/AndroidStudyGroup/conferences/pulls?q=is%3Apr+author%3Acketti+created%3A2021) - added a few events; but as one of the maintainers, I mostly click the "Merge pull request" button
- [android/storage-samples](https://github.com/android/storage-samples/pulls?q=is%3Apr+created%3A2021+author%3Acketti) - various bug fixes
- [c-base/c-base-org-lektor](https://github.com/c-base/c-base-org-lektor) - [uwekamper](https://github.com/uwekamper) and I rewrote the [c-base website](https://c-base.org/)
- [Element Android](https://github.com/vector-im/element-android/pull/3965) - fixed the preview when sharing images
- [ErikHellman/base45-kotlin](https://github.com/ErikHellman/base45-kotlin/pull/1) - small improvements
- [EventFahrplan](https://github.com/EventFahrplan/EventFahrplan/pulls?q=is%3Apr+created%3A2021+commenter%3Acketti) - removed unused code and reviewed a couple of pull requests
- [FastAdapter](https://github.com/mikepenz/FastAdapter/pull/985) - added a 'reorder via drag & drop' screen to the sample app; made small changes to the library to support this use case
- [jakewharton.com](https://github.com/JakeWharton/jakewharton.com/pull/43) - I create pull requests to fix typos in blog posts if the site is built from a Git repository 😀
- [MaterialDrawer](https://github.com/mikepenz/MaterialDrawer/pull/2716) - small fix to support loading images via URIs using a custom scheme
- [signald](https://gitlab.com/signald/signald/-/merge_requests?scope=all&state=all&author_username=cketti) - small changes and fixes
- [signald.org](https://gitlab.com/signald/signald.org/-/merge_requests?scope=all&state=all&author_username=cketti) - fixed some links
- [SlimSocial for Twitter](https://github.com/rignaneseleo/SlimSocial-for-Twitter/pull/20) - fixed a bug in the code handling the Share intent


## Donations to open source projects

Aside from recurring donations set up the previous year, 2021 was the year of spontaneous donations. I mostly sponsored projects and individuals because I liked their work, not because I was using the software or service they had created.

- [Dino](https://dino.im/)
- [Fosstodon](https://fosstodon.org/)
- [gitea](https://gitea.io/)
- [KeePassXC](https://keepassxc.org/)
- [Let's Encrypt](https://letsencrypt.org/)
- [Liberapay](https://liberapay.com/)
- [Matrix](https://matrix.org/)
- [pixelfed](https://pixelfed.org/)
- [Simply Secure](https://simplysecure.org/)
- [The Tor Project](https://www.torproject.org/)
- [Thunderbird](https://www.thunderbird.net/)
- [Tusky](https://tusky.app/)
- [WebRTC.rs](https://webrtc.rs/)

The donations to The Tor Project, WebRTC.rs, pixelfed, Simply Secure, and gitea I made via [FundOSS](https://fundoss.org/share/660b36a26c).

I also sponsored the following individuals:
- [bleeptrack](https://www.bleeptrack.de/) - creates art using code
- [chrisrhymes](https://github.com/chrisrhymes) - creator of the [bulma-clean-theme](https://github.com/chrisrhymes/bulma-clean-theme) Jekyll theme I used for the Jitsi Hacks website
- [johnjohndoe](https://github.com/johnjohndoe) - maintainer of the [EventFahrplan](https://github.com/EventFahrplan/EventFahrplan) Android app
- [Mariatta](https://github.com/Mariatta) - does lots of things in the Python community; gave an inspiring talk at the [Global Maintainer Summit 2021](https://globalmaintainersummit.github.com/)
- [mikepenz](https://github.com/mikepenz) - creator of the [MaterialDrawer](https://github.com/mikepenz/MaterialDrawer) and [FastAdapter](https://github.com/mikepenz/FastAdapter) libraries we use in K-9 Mail
- [Slavi Pantaleev](https://liberapay.com/s.pantaleev/) - creator of [matrix-docker-ansible-deploy](https://github.com/spantaleev/matrix-docker-ansible-deploy), which I use to manage my Matrix server


## Financials

In 2020 my main source of income was a grant from the [Prototype Fund](https://prototypefund.de/en/). But applying for grants and the associated paperwork is… not fun. So in 2021 I tried something else.

### K-9 Mail

On [I love Free Software Day](https://fsfe.org/activities/ilovefs/) I published the blog post [K-9 Mail is looking for funding](https://k9mail.app/2021/02/14/K-9-Mail-is-looking-for-funding). I was asking users for money so I could dedicate 80% of my time to working on the app. 

The post was picked up by various news sites and in February alone K-9 Mail's Liberapay account received around 19,000 EUR 🎉

At the end of the year a total of **51,002.55 EUR** had been donated via Liberapay, GitHub Sponsors and bank transfers. Check out [Donations in 2021](https://k9mail.app/2022/01/07/Donations-in-2021) for more details.


### Liberapay

In 2021 my [personal Liberapay account](https://liberapay.com/cketti) received **58.46 EUR** from 5 patrons 💖

### Total

The donations for K-9 Mail together with the donations to my personal Liberapay account add up to **51,061.01 EUR**.


## Reflections

If it was a regular job, a salary of €51k would be very disappointing to me. But it is not. I get to do what I love every day. And on days where I don't feel the love, I just do something else.  
It's great to see that what I create is useful to others. It's awesome that so many people find this work valuable enough to give money 💖

My plan was to use 80% of my time to work on K-9 Mail. But in 2021 it was much more than that. It hasn't been a problem so far. But I think I need to find a healthier balance.

I feel relieved that I finally managed to release a new stable version of K-9 Mail. Hopefully it won't be another 3 years until the next release 🤞


## Plans for 2022

The goals for 2022 are simple. Keep working on K-9 Mail to make the app better. And convince enough people to sponsor my open source work, so I can keep doing this full time.

If you want to help, [become a sponsor](https://cketti.de/sponsor/) 😃


## Thanks

None of this would have been possible without the people donating to the K-9 Mail project and the ones sponsoring me directly. Thank you! ❤️
