---
layout: single
title: "animation 관련"
categories: coding
tag: [css, styled-component]
toc: true
author_profile: false
sidebar:
 nav: "docs"
typora-root-url: ../
---

```typescript
export const shake = keyframes`
  0% {
    transform: translate(0, 0);
  }
  25% {
    transform: translate(-0.5rem, 0);
  }
  70% {
    transform: translate(0.5rem, 0);
  }
  100% {
    transform: translate(0, 0);
  }
`;
 
export const shakeSection = styled.div`
	animation: ${shake} 200ms 2;
`
```

keyframe은 animation의 이름을 정의하는 것이다. 이름을 정의할 때 특수문자, 숫자로 시작하는 이름은 유효하지 않는다.

shake로 정의한 이름을 적용하고 싶은 태그에 적용하면 된다. 



![제목 없는 동영상 - Clipchamp로 제작](/images/2023-06-05-animation/제목 없는 동영상 - Clipchamp로 제작.gif)