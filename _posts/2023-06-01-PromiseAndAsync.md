---
layout: single
title: "Promise와 async 관련"
categories: coding
tag: [React, javascript]
author_profile: false
sidebar:
 nav: "docs"
---

```javascript

const exFunction1 = (num) => {
    return num;
}
const exFunction2 = (num) => {
    return num;
}
const exFunction3 = (num) => {
    return num;
}

// Promise Function
const promiseFunction = () => {
  return new Promise((resolve, reject) => {
    exFunction1(1, (err, data) => {
      if (err) {
        reject("exFunction1 error", err);
      } else {
        exFunction2(data + 1, (err, data) => {
          if (err) {
            reject("exFunction2 error", err)
          } else {
            exFunction3(data + 1, (err, data) => {
              if (err) {
                reject("exFunction3 error", err);
              } else {
                resolve(data); // return 3;
              }
            });
          }
        });
      }
    });
  });
}

// Async Function
export async function AsyncFunction() {
    await data1 = exFunction1(1);
    await date2 = exFunction2(data1 + 1);
    await data3 = exFunction3(data2 + 1);
    
    return data3; // return 3;
}
```

위와 같이 작성하면 Promise나 async 둘 다 위에서 아래로 순차적으로 함수가 실행되지만 차이점이 존재한다.

1. Promise 함수는 Promise 함수 내부에서 error를 발생시킨다. (함수 내부에 reject로 error처리)

2. Async 함수는 Async 함수를 호출한 곳으로 error를 던진다. (함수 내부에 error처리가 따로 없음)
3. 개인적인 생각으로는 Promise보다 async의 코드가 가독성이 훨씬 좋고, 간결하다.
4. 하지만, Async는 Promise와 다르게 어느 함수에서 error가 발생했는지 확인하는 방법을 모르겠다. 더 연구가 필요하다.



## Try/Catch와 async/await를 사용하여 가독성이 좋은 코드 작성

 ```javascript
 ```



async 함수를 사용하여 처리하면 함수 앞에 await 가 붙은 함수가 실행 완료 될 때까지 기다려주고 함수 실행이 완료되면 다음 함수가 실행되므로 순차적으로 함수를 실행시켜야 할 때 사용하기 좋다. 

 error처리를 해놓은 Promise 함수들을 위와 같이 async 함수 내부에 작성하여 처리한다면 위에서 아래로 순차적으로 함수가 실행되다가 error가 잡힐 시, 어느 함수에서 어떤 error가 발생했는지 확인 할 수 있는 코드를 작성 할 수 있다.



