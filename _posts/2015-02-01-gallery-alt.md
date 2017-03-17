---
author: someone
layout: post-full
type: gallery
featimg: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
title: Gallery Alternative
tags: [gallery, image]
category: [image]
gallery:
    - images:
      - filename: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
        alttext: Bloom Flat
      - filename: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
        alttext: Bloom
      - filename: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
        alttext: Blossom in a Star
      - filename: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
        alttext: Blossom
      - filename: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
        alttext: Bubbly Bloom
      - filename: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
        alttext: Rays of Gold
      - filename: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
        alttext: Exotic
      - filename: http://upload-images.jianshu.io/upload_images/1271438-c9a2c15f26c9aafe.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
        alttext: 我是图片标题
---

An alternative to the simple gallery would be this version, which displays the post ins a lightbox.
The setup basically is the same, the include makes all the difference.

Galleries are defined in a data-sheet, set type and gallery-id in front matter and include `gallery_lightbox.html` within the content.
<br>

###### front matter

```yml
---
layout: post-full
type: gallery
gallery:
    - images:
      - filename: gallery-1.jpg
        alttext: Bloom Flat
      - filename: gallery-2.jpg
        alttext: Bloom
      - filename: gallery-3.jpg
        alttext: Blossom in a Star
      - filename: gallery-4.jpg
        alttext: Blossom
      - filename: gallery-5.jpg
        alttext: Bubbly Bloom
      - filename: gallery-6.jpg
        alttext: Rays of Gold
      - filename: gallery-7.jpg
        alttext: Exotic
      - filename: gallery-8.jpg
        alttext: Filled out
---
```
<br>

###### post content

``` liquid
{% raw  %}
{% include gallery_lightbox.html %}
{% endraw %}
```

{% include gallery_lightbox.html %}