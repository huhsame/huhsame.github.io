---
title: "Managing Dynamic Shared State #1"
date: 2019-06-25 00:33:31 +0900
categories: book
---

The goal of a networked virtual environment is to provide users with the illusion that they are all seeing the same things and interacting with each other within that virtual space.
A key consideration is how to make sure that the participating hosts(여기서 각 참여자를 호스트라고 함) keep a consistent view of this dynamic shared state.
**Dynamic shared state** constitutes the changing information that multiple machines must maintain about the vet-VE. and what and who is scurrently participating in the VE, locations and current behaviors.
 
 계속 변하는 인포메이션을 실시간으로 같이 공유해야한다. 
 정확한 dynamic shared state는 진짜같은 환경을 만드는 핵심역할이다. 
 
 The dynamic shared state provides common context that makes the virtual environment into a collaborative or competitive experience.
 
 
## contents
 - Consistency-throughput tradeoff
 - Maintain shared state
    1. shared repositories
    2. frequent broadcast
    3. state prediction

## The Consistency-Throughput Tradeoff

대부분의 경우 1명이 변경한 정보가 다른 여러명에게 mirrored 된다. 
하지만 이때 메세지 패킷이 전송되는 시간이 발생한다(network latency)
메세지가 전송되는 10ms 동안은 서로 다른 정보를 가지고 있다 (consistency 깨진 상태)


```
It is impossible to allow dynamic shared state 
to change frequently and guarantee 
that all hosts simultaneously access identical versions of that state.
```
The net-VE cannot support both dynamic behavior and absolute consistency.


### Proof of the Tradeoff

`absolute consistency` 를 보장하려면 모든 애들이 정보를 잘 받앗는지 매번 검사하고 받을 때 까지 기다려야한다.
```
Delay = transmission time + network latency + wating for ack + possible retransmission
```
이를 위해서 update rate를 낮춰야한다. 하지만 너무 낮으면 인터랙티브한 netVE가 되기 힘들다.

`week consistency` 는 업데이트했을때 나말고 다른애들도 다 업데이트되었는지 몰라서 확인 해줘야한다. 
```
Delay = transmission time + network latency
```

### Design Implications of the Tradeoff
업데이트를 햇으면 원본이 다른애들을 다 받았는지 확인하거나 다음 업데이트를 할건지 결정해야한다. 

```
Available network bandwidth must be allocated 
between messages for updating the dynamic shared state 
and messages for maintaining a consistent view of that dynamic shared state among participants in the net-VE.
```
update를 위한 메세지 + consistency를 위한 메세지

the net-VE must tolerate some inconsistency in the shared state updates seen by each host.
네트워크 환경이 안정적일 땐 strong, 머신마다 차이가 날때는 eventual.

