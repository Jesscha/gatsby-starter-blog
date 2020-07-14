---
title: Daily Study Logging43 - TCP/IP 4 layer
date: "2020-07-04T12:13:32.169Z"
description: TCP/IP
tags: ["network", "studylog"]
---

## TCP/IP 4 Layer가 뭔지 알아보자

TCP/IP는 네트워크 상에서 컴퓨터가 소통하기 위해 사용하는 프로토콜이다. 프로토콜이란 서로 어떤 식으로 소통을 할지 미리 정해 놓은 규약이라고 할 수 있다. 쉽게 예를 들면 한국인과 일본인이 서로 만나서 앞으로 영어로 이야기 하자는 규약을 맺는다고 생각해 보자. 이때 영어를 사용하기로 한 것이 바로 프로토콜이 된다.

TCP/IP는 데이터가 어떻게 인터넷상에서 교환되는지를 구체화 한다. 구체적으로 교환되는 데이터가 어떻게 패킷으로 나누어 지고, 처리되고, 전송되고, 라우팅되고 목적지에 전달되는지를 정의한다. TCP/IP는 중앙 집중적인 통제를 매우 조금 요구하기에 네트워크를 구성하는 디바이스에 문제가 생긴다고 해도 자동으로 네트워크를 회복시키는 능력이 있다.

다른 컴퓨터와 소통을 하는 과정을 TCP/IP 4 layer모델을 통해서 설명한다. 거의 모든 인터넷 소통은 TCP/IP 4 layer를 거친다.

1. 응용계층(Application Layer), 응용프로그램을 구현 하는데 사용하는 계층이다. 인터넷 주소 창에 url을 치고 클릭하는 행위는 Application Layer에서 일어난다.
2. 전송계층(Transfort Layer), 통신하는 컴퓨터간의 연결을 제어하는 Layer다. 응용계층에서 결정된 전송하고자 하는 데이터를 쪼개고 순서를 붙여서 다음 레이어로 전달한다. 이렇게 순서가 붙은 것을 TCP header라고 한다.
3. 인터넷 계층(Internet Layer), 나누어진 데이터 패킷에 IP를 붙인다. 어떤 IP에서 이 패킷이 전송되었고, 어디로 전달되어야 하는지를 IP header에 기록해 놓는다.
4. 네트워크 액세스 계층(Network Access Layer or Network Interface Layer), 앞선 단계에서 만들어진 데이터 패킷이 실제로 전달되는 레이어다.

이렇게 전달된 패킷은 받는 측에서 역순으로 해석이된다. 네트워크 엑세스계층을 통해 전달받고, 인터넷 계층에서 이 패킷을 받는 IP 주소가 맞는지 확인하고 전송계층에서 나눠져 들어오는 패킷을 이어 붙이고 응용계층에서 이렇게 주어진 데이터를 사용한다.