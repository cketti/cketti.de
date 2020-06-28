---
layout: post
title: content:// URIs and OkHttp
lead: Learn how to use OkHttp to upload documents on Android when all you have is a content:// URI.
tags: ["android", "content-uri"]
readtime: true
cover-img:
  - "/img/content-uris-and-okhttp/christa-dodoo-MldQeWmF2_g-unsplash.jpg" : "Photo by <a href='https://unsplash.com/@krystagrusseck?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText'>Christa Dodoo</a> on <a href='https://unsplash.com/photos/MldQeWmF2_g'>Unsplash</a>"
share-img: /img/content-uris-and-okhttp/christa-dodoo-MldQeWmF2_g-unsplash.jpg
---

Over a year ago I typed up an implementation of [OkHttp](https://square.github.io/okhttp/)'s [`RequestBody`](https://square.github.io/okhttp/4.x/okhttp/okhttp3/-request-body/) that supports Android's `content://` URIs. I called it [`ContentUriRequestBody`](https://gist.github.com/cketti/8ac927509787d7085a5ef8f866806f0f) and made it available as a [Gist](https://gist.github.com/).
The other day [a comment on the Gist](https://gist.github.com/cketti/8ac927509787d7085a5ef8f866806f0f#gistcomment-3313081) made me realize that this code might be helpful to more people than the person for whom it was originally created; probably more so when accompanied by some form of explanation. So here we go.

## Uploading a document

Using Android's Storage Access Framework to allow the user to select a document is fairly straight-forward. We do it like this:

```kotlin
val openDocumentIntent = Intent(Intent.ACTION_OPEN_DOCUMENT).apply {
    type = "*/*"
    addCategory(Intent.CATEGORY_OPENABLE)
}

startActivityForResult(openDocumentIntent, REQUEST_UPLOAD_DOCUMENT)
```

When the user has selected a document we get the result in `onActivityResult()`. The data field of the result `Intent` contains a `content://` URI that can be used to access its contents.

We'll get back to this in a minute. First, let's look at how to upload a file using an HTTP POST request with OkHttp.

```kotlin
val request = Request.Builder()
    .url("https://domain.example/upload")
    .post(requestBody)
    .build()

val response = okHttpClient.newCall(request).execute()
```

So, we need a `RequestBody` instance that provides the content to be uploaded. If we look closer, we notice it is an abstract class and none of the implementations that come with OkHttp seem to fit our use case. But that can easily be fixed. There's only two functions we need to implement:

```kotlin
class ContentUriRequestBody(
    private val contentResolver: ContentResolver,
    private val contentUri: Uri
) : RequestBody() {

    override fun contentType(): MediaType? {
        val contentType = contentResolver.getType(contentUri)
        return contentType?.toMediaTypeOrNull()
    }

    override fun writeTo(bufferedSink: BufferedSink) {
        val inputStream = contentResolver.openInputStream(contentUri)
            ?: throw IOException("Couldn't open content URI for reading")

        inputStream.source().use { source ->
            bufferedSink.writeAll(source)
        }
    }
}
```

The **`contentType()`** function provides the media type (also called MIME type, or content type) for the content, e.g. `image/jpeg` or `text/plain`. Our `content://` URI can be queried for the media type of the document. This is done by calling [`ContentResolver.getType(contentUri)`](https://developer.android.com/reference/android/content/ContentResolver#getType(android.net.Uri)).

To send the actual bytes that make up the document the **`writeTo()`** function is called by OkHttp. Using [`ContentResolver.openInputStream()`](https://developer.android.com/reference/android/content/ContentResolver#openInputStream(android.net.Uri)) gives us a `java.io.InputStream` instance to read the data from.
OkHttp is also using streams to read data from and write data to the network. But not the `java.io` API. Instead it is built on top of a library called [Okio](https://square.github.io/okio/), that implements the same concept, but in a much nicer way. Fortunately, Okio comes with an easy way to treat `java.io.InputStream` and `java.io.OutputStream` like the corresponding types in the Okio world, [`Source`](https://square.github.io/okio/2.x/okio/okio/-source/) and [`Sink`](https://square.github.io/okio/2.x/okio/okio/-sink/).
When calling the `writeTo()` function, OkHttp is handing us a `BufferedSink` and expects us to write the data to it. Since the document could be very large, we don't want to read all of the bytes into memory and the write them to the `BufferedSink`. Instead we do what streams were designed to support: read a small amount of bytes from the document into memory, then write them to the `BufferedSink` so OkHttp can send them over the network. This step is repeated until we have read and subsequently written all of the document bytes. But because copying data from a source stream to a destination stream is such a common operation, there's functionality in Okio that does all the heavy lifting for us. All we need to do is call the extension function `source()` to turn the `InputStream` we got from `ContentResolver.openInputStream()` into a `Source`. Then we call [`BufferedSink.writeAll(Source)`](https://square.github.io/okio/2.x/okio/okio/-buffered-sink/write-all/) and Okio will copy all bytes from the source to the sink.

And that's about it. This is more or less everything you need to send content referenced via a `content://` URI as body of an HTTP request using OkHttp.

## Writing downloaded content to a document

Downloading content and writing it to a document is even easier because it doesn't require us to extend a class. Displaying the system UI to allow the user to select a location and name for a new document is done like this:

```kotlin
val openDocumentIntent = Intent(Intent.ACTION_CREATE_DOCUMENT).apply {
    type = "image/jpeg"
    addCategory(Intent.CATEGORY_OPENABLE)
    putExtra(Intent.EXTRA_TITLE, "kitten.jpeg")
}

startActivityForResult(openDocumentIntent, REQUEST_DOWNLOAD_DOCUMENT)
```

Again, we get a content URI in the result Intent delivered to `onActivityResult()`. We can then make an HTTP request and write the response to the document.

```kotlin
val request = Request.Builder()
    .url("https://placekitten.com/300/300")
    .build()

okHttpClient.newCall(request).execute().use { response ->
    if (response.isSuccessful) {
        response.body!!.source().use { bufferedSource ->
            val outputStream = contentResolver.openOutputStream(contentUri)
                ?: throw IOException("Couldn't open content URI")

            outputStream.sink().use { sink ->
                bufferedSource.readAll(sink)
            }
        }
    }
}
```

It works similar to uploading, only this time we get a `java.io.OutputStream` instance when calling [`ContentResolver.openOutputStream()`](https://developer.android.com/reference/android/content/ContentResolver#openOutputStream(android.net.Uri)) with our `content://` URI. Again, there's a handy extension function to turn this into one of Okio's types, in this case `Sink`. The API surface of Okio's `Source` and `Sink` types is rather limited. The really useful functionality comes with `BufferedSource` and `BufferedSink`. We could easily turn our `Sink` into a `BufferedSink` by using the extension function `buffer()`. Then we'd be able to call `BufferedSink.writeAll(Source)` like we did when uploading a document. But because OkHttp is already handing us a `BufferedSource`, we can also call [`BufferedSource.readAll(Sink)`](https://square.github.io/okio/2.x/okio/okio/-buffered-source/read-all/) to copy all bytes from the source to the sink.

## Sample app

I hope this post has helped you to understand how to make OkHttp play nice with `content://` URIs. Of course code snippets in blog posts always seem to be missing some crucial bits of information. So I created a small sample app that you can play around with: [OkHttpWithContentUri](https://github.com/cketti/OkHttpWithContentUri)
