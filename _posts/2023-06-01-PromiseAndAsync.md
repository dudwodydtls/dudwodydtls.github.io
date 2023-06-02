---
layout: single
title: "Promise, async/await, try/catch"
categories: coding
tag: [React, javascript]
author_profile: false
sidebar:
 nav: "docs"
---

```javascript
// exFunction
const exFunction1 = (num) => {
    return num;
}
const exFunction2 = (num) => {
    return num;
}
const exFunction3 = (num) => {
    return num;
}

// Promise
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

// Async/await & try/catch
export async function AsyncFunction() {
    try {
        data1 = await exFunction1(1);
        date2 = await exFunction2(data1 + 1);
        data3 = await exFunction3(data2 + 1);
    } catch(err) {
        console.log("err 발생", err);
    } finally {
    	return data3; // return 3;    
    }
}
```

**promise로 작성한 코드와 try/catch, async/await로 작성한 코드는 똑같이 작동한다. 

**개인적인 생각으로는 Promise보다 try/catch, async/await로 작성하는 방식이 가독성이 좋고 코드도 간결하기 때문에 더 좋은 작성 방법이라고 생각한다.

