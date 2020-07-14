---
title: Daily Study Logging44 - 네트워크 일반 면접 질문
date: "2020-07-06T12:13:32.169Z"
description: 네트워크 일반
tags: ["network", "studylog"]
---

## Multi-Thread 서버에 대해 설명하시오

- 프로세스: 컴퓨터가 어떤 일을 하고 있는 상태, 코어가 여러개 있으면 여러개 동시 진행, 아니면 컨텍스트 스위칭으로 여러개의 일을 돌아가면서 처리, 컴퓨터는 프로세스마다 사용할 수 있는 자원을 할당함
- 스레드: 한 프로세스안에서 수행되는 작업, 각 스레드는 컴퓨터의 자원을 공유함
- 하나의 프로세스에서 여러개의 스레드 단위로 나누어 다중 처리를 하는 방식의 서버를 멀티스레드 서버라고 함
- 싱글 스레드 서버를 사용하는 경우, 서버에서 첫번째 요청에 대한 작업이 끝나기 전에, 두번째 요청이 들어온다면 앞선 작업이 끝날 때까지 대기해야함
- 프로세스를 새로 만드는 멀티 프로세스 방식을 사용하는 것보다 더 작고 빠르게 동작함
- 단, 독립된 프로세스 단위로 동작하지 않아 디버깅이 힘들고, 한 스레드의 문제가 전체 프로세스에 문제를 줄수 있다는 단접이 있음

## 소켓 이란

- 2개 디바이스간의 커뮤니케이션 엔드포인트
- 네트워크 상에서 2개의 컴퓨터가 소통하기 위해서는 각 엔드포인트에 소켓이 필요함
- 두 컴퓨터의 소켓이 연결되면 서로 데이터를 주고 받을 수 있게 됨
- 서버는 처음부터 소켓을 가지고 있지는 않고, 클라이언트에서 요청이 오면 서버소켓이 리퀘스트를 받고 소켓을 새로 만든다.

## 프록시 서버의 기능에 대해 설명하시오

- 프록시 서버는 유저를 대신해 인터넷에서 데이터를 받아오는 역할을 하는 서버다.
- 프록시는 클라이언트의 프라이빗 아이피를 퍼블릭으로 바꿔줌
- 프록시는 웹서버에서 대답을 받아서 응답을 신청한 클라이언트에게 돌려줌
- 악의적 트래픽을 막아줌, 해커가 특정 클라이언트에 접근해서 악의적 행동을 못하게 함 (물론 더 복잡하겠지만, 프록시 서버까지 해킹할수도 있다.)
- 웹사이트를 차단할수 있음, 예를 들어 직원들이 회사 컴퓨터로 성인 사이트를 방문하는 것을 막을 수 있음 또한, 이 직원들의 활동을 기록 할 수 있음
- 퍼포먼스를 향상 시킬수 있음, 이것이 제일 중요한 기능, 프록시 서버에서 특정 요청에 대한 응답을 캐싱해서 같은 요청이 오는 경우 그 응답을 돌려준다. 인터넷 밴드윗을 아낄 수 있다.

## TCP 3-way Handshake란?

- TCP는 장치들 사이의 논리적 접속을 성립하기 위하여, 3-way handshake를 사용함
- TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에, 정확한 정보 전송을 위하여 상대 컴퓨터와 세션을 수립하는 과정

### 진행 과정

1. A 클라이언트는 B 서버에 접속을 요청하는 SYN 패킷을 보낸다. SYN 패킷을 보낸뒤, 클라이언트 A는 SYN_SENT 상태가 된다.
2. B 서버는 SYN 요청을 받고 요청을 수락한다는 ACK와 SYN가 모두 담긴 설정된 패킷을 발송하고, A가 다시 ACK로 응답하기를 기다린다. B의 상태는 SYN_RECIEVED 상태가 된다.
3. A 클라이언트는 B서버에게 ACK를 보내고 이후부터는 연결이 이루어지고 데이터가 오간다.ACK를 받은 B 서버의 상태는 ESTABLISHED가 된다.

## 4-way Handshake란?

- TCP연결로 생겨난 세션을 종료하기 위해 수행되는 절차

### 진행과정

1. 클라이언트가 연결을 종료하겠다는 FIN 플래그를 전송한다.

2. 서버는 일단 해당 클라이언트의 종료 요청을 받았다는 의미로 ACK를 클라이언트에게 전송한다. 그리고 서버 자신의 통신이 끝날때 까지 기다리는데, 이 상태가 TIME_WAIT상태다.

3. 서버 통신이 끝났으면 연결이 종료되고 클라이언트에게 FIN을 전송한다.
4. 클라이언트는 종료 메시지를 받았다는 ACK를 서버에 전송한다.

- 클라이언트에서 세션을 종료시킨 뒤에 뒤늦게 도착하는 패킷이 있다면, 이 패킷은 유실될 가능성이 있음, 따라서 클라이언트는 FIN을 수신하더라도 일정시간동안 세션을 남겨 놓고 잉여패킷을 기다리는 과정을 거침

## session과 쿠키의 개념

### 쿠키와 세션을 사용하는 이유

- HTTP 프로토콜의 특징이자 약점을 보안하기 위함
- HTTP 프로토콜 환경에서 서버는 클라이언트가 누구인지 확인해야 함, HTTP 프로토콜은 connectionless, stateless하기 때문

### 쿠키

- 클라이언트 로컬에 저장되는 작은 key-value로 이루어진 데이터 파일
- 인증 유효시간을 명시할 수 있음, 유효시간이 정해지면 브라우저가 종료되어도 인증이 유지됨
- 클라이언트에 300개까지 쿠키 저장 가능, 하나의 도메인당 20개 값만을 가질수 이음,하나의 쿠키는 4kb

#### 쿠키 동작방식

1. 클라이언트가 페이지를 요청
2. 서버에서 쿠키를 생성
3. HTTP 헤더에 쿠키를 포함시켜 응답
4. 브라우저가 종료되어도 쿠키 만료 기간이 있다면 클라이언트에서 보관하고 있음
5. 같은 요청을 할경우 HTTP 헤더에 쿠키를 함께 보냄
6. 서버에서 쿠키를 읽어 이전 상태 정보를 변경할 필요가 있을 때, 쿠키를 HTTP 헤더에 포함시켜 응답

### 세션

- 쿠키 기반이지만, 사용자 정보를 서버측에서 관리함
- 클라이언트를 구분하기 위해 세션 ID를 부여하며, 웹 브라우저가 서버에 접속해서 브라우저가 종료될 때까지 인증상태를 유지
- 클라이언트가 리퀘스트를 보내면 서버가 해당 클라이언트에게 유일한 ID를 부여하는데 이것이 세션 ID
- 사용자에 대한 정보를 서버에 두기 때문에 쿠키보다 보안에 좋지만, 사용자가 많아질수록 서버 메모리를 많이 차지하게 됨
- 동접자 수가 많은 웹사이트의 경우, 서버 성능저하의 요인이 된다.

#### 세션 동장방식

- 클라이언트가 서버 접속시 세션 ID를 발급받음
- 클라이언트는 세션 ID에 대해 쿠키를 사용해서 저장하고 가지고 있음
- 클라이언트가 서버에 요청을 할때, 이 ID를 서버에 전달함
- 서버는 세션 ID를 전달받아 별다른 작업 없이 세션 ID로 세션에 있는 클라이언트 정보를 가져옴
- 클라이언트 정보를가지고 서버요청을 처리하여 클라이언트에게 응답함

### 쿠키와 세션의 차이

- 세션도 쿠키를 사용하기에 동작원리도, 수행하는 역할도 비슷함
- 사용자의 정보가 저장되는 위치가 다름, 쿠키는 서버의자원을 사용하지 않고 세션은 서버의 자원을 사용함
- 보안면에서 세션이 더 우수하며, 요청속도는 쿠키가 세션보다 빠름, 세션은 서버의 처리가 필요하기 때문
- 쿠키는 클라이언트 로컬에 저장되기 때문에 변질되거나 request할때 스니핑 당할 우려가 있지만, 세션은 세션 ID만 저장할 뿐 서버에서 그 외 데이터를 처리하기에 보안적으로 더 뛰어남
- 쿠키는 만료 기한을 넉넉히 잡으면 기한이 만료되거나 쿠키를 삭제할때까지 유지됨, 세션은 브라우저 종료시 만료시간 관계없이 삭제됨

### 캐시와의 차이

- 캐시는 이미지나, css, js 파일 등을 브라우저나 서버 앞단에 저장해 놓고 사용하는 것

## SQL Injection이란?

- SQL에 사용되는 인풋에 명령어를 악의적으로 삽입하는 공격을 말한다.

### 예시

- `INSERT INTO students (이름) VALUES ('학생 이름');`이러한 SQL문으로 학생 데이터를 저장하는 학생기록부가 있다고 생각해 보자
- 학생 이름 란에 ');DROP TABLE students; 를 넣으면 위의 코드는 `INSERT INTO students (이름) VALUES ('');DROP TABLE students;);` 가 된다.
- 학생 데이터를 저장하고 테이블을 지우는 명령어가 수행이 되는 것이다.

### 방지

- 유저에게 받은 값을 직접 SQL로 넘겨서는 안됨
- 입력이 의도치 않은 동작을 방지하는 이스케이핑을 해야 함
- DB에 유저별 접근권한과 사용가능한 명령어를 설정
- 클라이언트 측에서 입력을 받을때 폼 입력값을 한번 검증 후 서버엣서 한번더 값을 검증

## CSRF 와 XSS

### CSRF

- Cross Site Request Forgery, 사이트간 요청 위조 라는 뜻
- 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위를 특정 서버에 요청하도록 하는 방법

#### CSRF원리

- 서버는 유저를 브라우저 단위로 인식한다. 페이스북에 로그인 한뒤 새로운 탭을 열어보라 페이스북에 로그인 된 상태가 유지되는것은 이때문이다.
- 공격자는 사용자가 브라우저 인증이 된 상태에서 다른 요청을 보내도록 유도한다.
- 예를들어, 자신이 만든 웹사이트에 브라우저가 인증된 상태로 방문해서 특정 버튼을 클릭할때, 그 유저가 로그인 해 놓은 사이트에서 작업을 수행하는 명령을 보내도록 하는 것이다.
- 사용자가 버튼을 클릭했을때 눈에 보이는 UI에는 아무 이상이 없고 눈에 보이지 않는 부분에서 해당 요청이 일어나기에 사용자는 이를 확인할수 없다.
- 인증된 사용자의 브라우저에서 요청이 들어간 것이기 때문에 서버는 해당 요청을 정당한 것으로 받아들이고 작업을 수행한다.

#### CSRF예방

- reqeust의 요청이 같은 도메인에서 발생한 것인지를 체크한다. (개발할때 CORS 에러가 자주 발생하는 것은 CSRF를 막기 위함이다.)
- security token을 활용 한다. 사용자의 세션에 난수 값을 저장하고 사용자의 요청마다 해당 난수값을 포함시켜 전송시킨다. 백엔드단에서 요청을 받을 때마다 세션에 저장된 토큰 값과 요청 파라미터에 전달되는 토큰 값이 일치하는지 검증한다.

### XSS

- Cross-Site Scripting, 사이트간 스크립팅 이라는 뜻
- 사용자가 공격하려는 사이트에 악의적 스크립트를 심어두어 유저가 해당 사이트에 방문했을 시 해당 스크립트를 수행하도록 함
- 공격자는 브라우저에 있는 정보를 탈취할 수 있음, 쿠키 값을 탈취해 사용자인척 가장하고 활동하는 등의 공격 가능
- 공격자는 악성프로그램을 다운로드 시킬수 있음

#### XSS원리

- 웹브라우저는 HTML문서 상에서 `<script> </script>`태그를 만나면 그 안에 있는 자바스크립트 코드를 수행시킨다.
- 공격자가 특정 웹사이트의 콘텐츠에 위처럼 자바스크림트 코드를 집어 넣으면 사용자들은 그 코드를 다운로드 받고 수행하게된다.
- 예를 들어, 모든 유저가 볼 수 있는 덧글에 코드를 심어두면 (웹사이트에서 조치를 안한 경우) 그 댓글이 있는 페이지에 접근한 모든 유저는 해당 자바스크립트를 브라우저에서 수행하게 된다.

#### XSS대책

- 입력값 제한, 스크립트를 삽입하지 못하게 한다.
- 입력값 치환 XSS공격은 script 태그를 사용하기 때문에 태그문자(<>)등의 문자 입력시 문자참조(HTML entity)로 필터링하고 서버에서 브라우저로 전송시 문자를 인코딩하게 할 수 있다. 예를들어 "<"는 "\&lt;"로 변경된다.
- 사용자의 입력을 다시출력하는 것을 최대한 자제해야 한다.