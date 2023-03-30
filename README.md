# webSocket
* 기존의 단방향 HTTP 프로토콜과 호환되어 양방향 통신을 제공하기 위해 개발된 프로토콜
* 방화벽에 제약이 없으며 통상 WebSocket으로 불림
* 클라이언트가 접속 요청을 하고, 웹 서버가 응답한 후에 연결을 끊는 것이 아닌 connection 을 그대로 유지하고 클라이언트의 요청이 없어도 데이터를 전송할 수 있는 프로토콜
* 실시간을 보장하고, 변경 사항의 빈도가 잦을 때 주로 사용

### webSocket 열기 HandShake
클라이언트가 먼저 핸드셰이크 요청을 보내고 이에 응답을 서버가 클라이언트로 보내는 구조

# stomp (Simple Text Oriented Messaging Protocol)
* webSocket 위에서 동작하는 양방향 네트워크 프로토콜
* HTTP에서 모델링 되는 Frame 기반 프로토콜
* 클라이언트와 서버가 전송할 메시지의 유형, 형식, 내용들을 정의하는 메커니즘.
* pub / sub 구조로 되어있어 메시지를 전송하고 메시지를 받아 처리하는 부분이 확실히 정해져 있음
  * 개발자 입장에서 명확하게 인지하고 개발 가능
  * pub: 메시지 송신
  * sub: 메시지 수신
* 메세지의 헤더에 값을 줄 수 있어 헤더 값을 기반으로 통신 시 인증처리를 구현하는 것

## stomp 형식
```text
COMMAND
header1:value1
header2:value2

Body^@
```
* COMMAND: SEND, SUBSCRIBE
* HEADER: 기존의 WebSocket으로 구현이 불가능한 Header 작성 가능
  * Destination: 메세지를 보내거나 구독을 할 수 있음

### 예시
```text
SUBSCRIBE
destination: /sub/chat/room/5
---------------------------------------
SEND
content-type: application/json
destination: /pub/chat

{"chatRoomId": 5, "type": "MESSAGE", "writer": "clientB"}
---------------------------------------
MESSAGE
destination: /subscribe/chat/room/5

{"chatRoomId": 5, "type": "MESSAGE", "writer": "clientB"}
```

[출처]
1. https://dev-gorany.tistory.com/212
2. https://dev-gorany.tistory.com/235
3. https://supawer0728.github.io/2018/03/30/spring-websocket/