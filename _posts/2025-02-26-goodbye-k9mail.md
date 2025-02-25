---
layout: post
title: Goodbye K-9 Mail
lead: "Looking back on 15 years of working on K-9 Mail."
tags: ["opensource"]
readtime: true
---

**TL;DR:** I quit my job working on [Thunderbird for Android](https://www.thunderbird.net/mobile/) and [K-9 Mail](https://k9mail.app/) at MZLA.

My personal journey with K-9 Mail started in late 2009, shortly after getting my first Android device[^1]. The pre-installed Email app didn't work very well with my email provider. When looking for alternatives, I discovered K-9 Mail. It had many of the same issues[^2]. But it was an active open source project that accepted contributions. I started fixing the problems I was experiencing and contributed these changes to K-9 Mail. It was a very pleasant experience and so I started fixing bugs reported by other users. 

In February 2010, [Jesse Vincent](https://metasocial.com/@jesse), the founder of the K-9 Mail project, offered me commit access to the Subversion[^3] repository. According to my email archive, I replied with the following text:

> Thank you! I really enjoyed writing patches for K-9 and gladly accept your offer. But I probably won't be able to devote as much time to the project as I do right now for a very long time. I hope that's not a big problem. 

My prediction turned out to be not quite accurate. I was able to spend a lot of time working on K-9 Mail and quickly became one of the most active contributors. 

In 2012, Jesse hired me to work on [Kaiten Mail](https://kaitenmail.com/), a commercial closed-source fork of K-9 Mail. The only real differences between the apps were moderate changes to the user interface. So most of the features and bug fixes we created for Kaiten Mail also went into K-9 Mail. This was important to me and one of the reasons I took the job.

In early 2014, Jesse made me the [K-9 Mail project leader](https://groups.google.com/g/k-9-mail/c/6OzXyOoksf8/m/xrbvkd1xO8AJ)[^4]. With Kaiten Mail, end-user support was eating up a lot of time and eventually motivation to work on the app. So we stopped working on it around the same time and the app slowly faded away. 

To pay the bills, I started working as a freelancing Android developer[^5]. Maybe not surprisingly, more often than not I was contracted to work on email clients. Whenever I was working on a closed source fork of K-9 Mail[^6], I had a discounted hourly rate that would apply when working on things that were contributed to K-9 Mail. This was mostly bug fixes, but also the odd feature every now and then.

After a contract ended in 2019, I decided to apply for a grant from the [Prototype Fund](https://prototypefund.de/) to work on adding JMAP support to K-9 Mail[^7]. This allowed me to basically work full-time on the project. When the funding period ended in 2020, the COVID-19 pandemic was in full swing. At that time I didn't feel like looking for a new contract. I filled my days working on K-9 Mail to mute the feeling of despair about the world. I summarized my 2020 in the blog post [My first year as a full-time open source developer](https://cketti.de/2021/01/14/my-first-year-as-a-full-time-open-source-developer/).

Eventually I had to figure out how to finance this full-time open source developer lifestyle. I ended up [asking](https://k9mail.app/2021/02/14/K-9-Mail-is-looking-for-funding) K-9 Mail users to donate so I could be paid to dedicate 80% of my time to work on the app. This worked out quite nicely and I wrote about it here: [2021 in Review](https://k9mail.app/2022/01/18/2021-in-Review).

I first learned about plans to create a Thunderbird version for Android in late 2019. I was approached because one of the options considered was basing Thunderbird for Android on K-9 Mail. At the time, I wasn't really interested in working on Thunderbird for Android. But I was more than happy to help turn the K-9 Mail code base into something that Thunderbird could use as a base for their own app. However, it seemed the times where we had availability to work on such a project never aligned. And so nothing concrete happened. But we stayed in contact.

In December 2021, it seemed to have become a priority to find a solution for the many Thunderbird users asking for an Android app. By that time, I had realized that funding an open source project via donations requires an ongoing fundraising effort. Thunderbird was already doing this for quite some time and getting pretty good at it. I, on the other hand, was not looking forward to the idea of getting better at fundraising.  
So, when I was asked again whether I was interested in K-9 Mail and myself joining the Thunderbird project, I said yes. It took another six months for us to figure out the details and [announce](https://k9mail.app/2022/06/13/K-9-Mail-and-Thunderbird) the news to the public.

Once under the Thunderbird umbrella, we worked[^8] on adding features to K-9 Mail that we wanted an initial version of Thunderbird for Android to have. The mobile team slowly grew to include another [Android developer](https://blog.thunderbird.net/2023/03/thunderbird-for-android-k-9-mail-february-progress-report/), then a [manager](https://blog.thunderbird.net/2024/07/thunderbird-for-android-k-9-mail-june-2024-progress-report/). While organizationally the design team was its own group, there was always at least one designer available to work with the mobile team on the Android app. And then there were a bunch of other teams to do the things for which you don't need Android engineers: support, communication, donations, etc. 

In October 2024, we finally released the [first version of Thunderbird for Android](https://blog.thunderbird.net/2024/10/thunderbird-for-android-8-0-takes-flight/). The months leading up to the release were quite stressful for me. All of us were working on many things at the same time to not let the targeted release date slip too much. We never worked overtime, though. And we got additional paid time off after the release ❤️ 

After a long vacation, we started 2025 with a more comfortable pace. However, the usual joy I felt when working on the app, didn't return. I finally realized this at the beginning of February, while being sick in bed and having nothing better to do than contemplating life.  
I don't think I was close to a burnout – work wasn't that much fun anymore, but it was far from being unbearable. I've been there before. And in the past it never was a problem to step away from K-9 Mail for a few months. However, it's different when it's your job. But since I am in the very fortunate position of being able to afford taking a couple of months off, I decided to do just that. So the question was whether to take a [sabbatical](https://en.wikipedia.org/wiki/Sabbatical) or to quit.  
Realistically, permanently walking away from K-9 Mail never was an option in the past. There was no one else to take over as a maintainer. It would have most likely meant the end of the project. K-9 Mail was always too important to me to let that happen.  
But this is no longer an issue. There's now a whole team behind the project and me stepping away no longer is an existential threat to the app.

I want to explore what it feels like to do something else without going back to the project being a foregone conclusion. That is why I quit my job at MZLA.

It was a great job and I had awesome coworkers. I can totally recommend [working](https://www.mozilla.org/en-US/careers/listings/?team=MZLA/Thunderbird) with these people and will miss doing so 😢

---

I have no idea what I'll end up doing next. A coworker asked me whether I'll stick to writing software or do something else entirely. I was quite surprised by this question. Both because in hindsight it felt like an obvious question to ask and because I've never even considered doing something else. I guess that means I'm very much still a software person and will be for the foreseeable future.

During my vacation I very much enjoyed being a beginner and learning about technology I haven't worked with as a developer before (NFC smartcards, USB HID, Bluetooth LE). So I will probably start a lot of personal projects and finish few to none of them 😃

I think there's a good chance that – after an appropriately sized break – I will return as a volunteer contributor to K-9 Mail/Thunderbird for Android.

But for now, I say: **Goodbye K-9 Mail** 👋

---

This leaves me with saying thank you to everyone who contributed to K-9 Mail and Thunderbird for Android over the years. People wrote code, translated the app, reported bugs, helped other users, gave money, promoted the app, and much more. Thank you all 🙏

---

[^1]: My youngest brother gave me his "old" [HTC Magic](https://en.wikipedia.org/wiki/HTC_Magic) ❤️
[^2]: This is not surprising when you learn that [K-9 Mail was forked from the AOSP Email app in October 2008](https://obra.livejournal.com/96524.html). 
[^3]: The K-9 Mail project was initially hosted on [Google Code](https://code.google.com/archive/p/k9mail/) where Git wasn't available at the time. 
[^4]: Jesse moved on to [build keyboards](https://keyboard.io).
[^5]: As a freelancer I rarely worked more than 30 hours a week. I made sure there was always enough time to work on K-9 Mail.
[^6]: There's surprisingly many of these forks around. Yet hardly any of the teams working on them ever contributed back to K-9 Mail 😞
[^7]: The app currently doesn't support JMAP. However, the [code](https://github.com/thunderbird/thunderbird-android/tree/be2af5c6a0bce08385fc3f654c1185ccf9db3859/backend/jmap) for basic JMAP support can be found in the repository.
[^8]: You can find monthly progress reports about this in the [mobile section of the Thunderbird blog](https://blog.thunderbird.net/category/mobile-news/).
