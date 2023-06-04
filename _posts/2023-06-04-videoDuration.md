---
layout: single
title: "input type file 로 선택한 비디오의 재생시간"
categories: coding
tag: [javascript, html]
toc: true
author_profile: false
sidebar:
 nav: "docs"
---

```javascript
const uploadVideo = (file) => {
    const video = await createVideoElement(URL.createObjectURL(file));
    return video.duration // 비디오 재생시간
}
```



파라미터로 넘어온 e.tartge.file을 createVideoElement와 URL.createObjectURL를 사용하여 비디오 객체를 만들어준다.

만든 비디오 객체 내부에 duration이 존재하므로 가져다 쓰면 된다.