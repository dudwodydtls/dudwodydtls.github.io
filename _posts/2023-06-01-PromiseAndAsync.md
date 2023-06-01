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
** 압축파일을 만들 때의 코드를 예시로 들어보았다.
// Promise Function

const promised_JsZipUtils_getBinaryContent = (path: string) => {
  return new Promise((resolve, reject) => {
    //JSZipUtils.getBinaryContent(): JSZip 라이브러리 함수
    JSZipUtils.getBinaryContent(path, (err, data) => {
      if (err) {
        reject(err);
      }
      resolve(data);
    });
  });
}

// Async Function

export async function generateAssetZip(filesData) {
  const data = await promised_JsZipUtils_getBinaryContent(path + '/' + filesData.FileData.id);
  // zip.file(): JSZip 라이브러리 함수
  zip.file(filesData.FileData.id + filesData.FileData.fileType, data, { 
    binary: true,
  });
  // generateAsync(): JSZip 라이브러리 함수
  const result = await zip.generateAsync({ type: 'blob' }); 
  const getMD5 = md5(result);
  return { result, getMD5 };
}
```

async 함수를 사용하여 처리하면 함수 앞에 await 가 붙은 함수가 실행 완료 될 때까지 기다려주고 함수 실행이 완료되면 다음 함수가 실행되므로 순차적으로 함수를 실행시켜야 할 때 사용하기 좋다. 

 error처리를 해놓은 Promise 함수들을 위와 같이 async 함수 내부에 작성하여 처리한다면 위에서 아래로 순차적으로 함수가 실행되다가 error가 잡힐 시, 어느 함수에서 어떤 error가 발생했는지 확인 할 수 있는 코드를 작성 할 수 있다.



