---
layout: single
title: "net socket 데이터 전송"
categories: coding
tag: [net socket]
toc: true
author_profile: false
sidebar:
 nav: "docs"
---

### net socket 서버를 생성하고 데이터를 전송하기

```javascript
	// net socket을 사용하기 위해 net 선언
	const net = require('net);
 	// net server 생성
    const server = net.createServer(function(socket) {
      // 연결됐음을 알리는 console.log
      console.log('CONNECTED: ' + socket.remoteAddress + ':' + socket.remotePort);
      // Stream 단위로 파라미터에 작성한 파일(exFile)을 읽는다. 
      // Stream단위로 읽을 경우 파일을 쪼개서 읽어서 전송한다. 대용량 데이터 전송 시 적합하다. 
      const fileStream = fs.createReadStream(exFile);

      // stream 단위로 읽은 파일을 pipe함수를 통해 전송한다.
      fileStream.pipe(socket);

      // Client와 통신이 끝난 후 실행됨.
      socket.on('close', function() {
        // 전송이 끝난 후 close 함수로 서버 종료
        server.close();
        console.log('Server Close');
      });

      // socket 통신 중 에러가 났을 경우 실행
      socket.on('error', function(err) {
        console.log(err);
      });
    });
```

