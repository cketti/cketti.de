---
layout: post
title: "Avoid Intent.resolveActivity()"
lead: "Android 11 limits the kind of information your app can retrieve about other apps. Learn why you might have to update your app even though you don't use PackageManager directly."
tags: ["android"]
cover-img:
  - "/img/avoid-intent-resolveactivity/caution.jpg" : "Photo by <a href='https://unsplash.com/@muukii?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText'>Muukii</a> on <a href='https://unsplash.com/photos/rtX4wxMEI2M'>Unsplash</a>"
share-img: /img/avoid-intent-resolveactivity/caution.jpg
readtime: true
---

Until recently [`PackageManager`](https://developer.android.com/reference/kotlin/android/content/pm/PackageManager) allowed every app to access information about every other installed app. While this information is vital for apps like launchers, most apps have no need to know which other apps are installed. So Android 11 makes it a little bit harder to retrieve this information. For more details see [Package visibility in Android 11](https://developer.android.com/preview/privacy/package-visibility).

Most apps should not be affected by this change because they don't need to perform any `PackageManager` queries. But, sadly, many apps contain code to start [implicit intents](https://developer.android.com/guide/components/intents-filters#Types) similar to this:

```kotlin
val intent = … // Some implicit intent, e.g. ACTION_VIEW

if (intent.resolveActivity(packageManager) != null) {
    startActivity(intent) // or startActivityForResult(…)
}
```

Due to the new limitations when targeting Android 11 the [`Intent.resolveActivity()`](https://developer.android.com/reference/kotlin/android/content/Intent#resolveActivity(android.content.pm.PackageManager)) call might now return `false` even though using `startActivity()` with the intent would work just fine.

To make this work you could add a `<queries>` entry to `AndroidManifest.xml` as explained in the [documentation](https://developer.android.com/preview/privacy/package-visibility). But my suggestion is to avoid using `Intent.resolveActivity()` in such a case.

## Why avoid Intent.resolveActivity()?

I always cringe when people recommend this "`resolveActivity()` then `startActivity()`" pattern. You're asking the system to perform the same operation twice. First "find the app to handle this Intent", then "find the app to handle this Intent and then start that app using this Intent".

The problem with code like this is that the environment might change between the two method invocations. There might be a suitable app installed when `resolveActivity()` is executed and it could be gone by the time `startActivity()` is executed. Granted, in practice it is very unlikely to run into this case. Still, I think we can do better.

## Catch ActivityNotFoundException instead

Instead of using `Intent.resolveActivity()` just call `startActivity()` and deal with [`ActivityNotFoundException`](https://developer.android.com/reference/kotlin/android/content/ActivityNotFoundException).

```kotlin
val intent = … // Some implicit intent

try {
    startActivity(intent)
} catch (e: ActivityNotFoundException) {
    // Display some error message
}
```

In the past, using one method over the other was mostly a matter of taste. With the changes in Android 11 this method has the big advantage that you don't have to add anything to `AndroidManifest.xml`. It just works.

## Always avoid Intent.resolveActivity()?

My advice only applies to this particular `startActivity()` use case. Of course `Intent.resolveActivity()` still has its uses. For example, you might want to hide a 'take picture' button if no camera app is installed. In that case `resolveActivity()` comes in handy.
