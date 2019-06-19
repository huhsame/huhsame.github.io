---
title: "The Promises and challenges of Networked Virtual Environments"
date: 2019-06-21 02:30:13 +0900
categories: swords, books, VR, net-VE
---

# Networked virtual environment
a software system in which multiple users interact with each other in real-time, even though those users may be located around the world
to provide user with **a sense of realism** to create an immersive experience.

### Common features
1. A shared sence of space: All participants have the illusion of being located in the same place.
2. A shared sence of presence: Each prticipant takes on a virtual persona, called avatar, which includes a graphical representation.
3. A shared sence of time: NEV should enable real-time interaction to occur.
4. A way to communicate: NEV enable communication among the participants - by gesture etc.
5. A way to share: NEV derives from users' abillity to interact realistically not only with each other but also with the virtual environment itself. _이게 무슨말_

물입 환경에서 서로 인터랙트 할 수 있고, 정보를 공유하고, 오브젝트들을 조작할 수 있는 여러명의 유저. 
telepresence : the illusion that other users are visible from remote locations. 

### components
1. graphics engines and displays : HMD
2. communication and control devices : controller, mic
3. processing systems: determines how and when to notify other participants of these changes.
4. data network : to exchange information.

# Challenges in NVE design and development
Traditional types of software rooled into a sing application
- Distributed systems: They musth contend with all of the challenges of managing network resources, data loss, network failure, and concurrency.
- Graphical applications: They must maintain smooth, real-time display frame retes and carefully allocate the CPU among rendering and other tasks.
- Interactive applications : They must process real-time data input from users. Users should see the virtual environment as if it exists locally, even though its participants are distributed ant multiple remote hosts.

components
- must integrate with database systems
- need to support user authentication
- must be able to log events in real-time to persistent storage.

### Network Bandwidth
NVEs rely on the data network to exchange information about the current state of the virtual environment. However, network capacity is a limited resource.

### Heterogeneity
Users do not have to access the same set of equipment.

### Distributed Interaction 
Users see each other's real-time activity and react to this information in real-time.
Network delays are particularly difficult to handle when multiple users or components interact with each other directly.
For example, collision detection, agreement, and resolution among participants.

### Real-time system design and resource management
Real-time interaction defines the process and thread architecture.
Many different tasks concurrently compete for use of the CPU, and unlike most systems, almost all of those tasks have hard real-time constraints.
Shared locks must be used to coordinate state updates (made for user input, arriving network packets, and virtual environment modeling and simulation) and state accesses (made for image generation, transmitting network packets, and virtual modeling and simulation)

### Failure Management
Designer must determine to what extent a failure may affect the excution of the application.
1. System stop : Failures may cause the entire NVE to terminate if the missing resource is critical to the NVE's execution.
2. System closure: Failures may not impact the existing user, but they may prevent the arrival of new users. 
_이미 인터랙션하고있는데 중간에 다른애가 들어오면 세이브파일 보여주면 안되고 템프 현재 꺼 보여줘야해_
3. System hindrance: Some failures may simply degrade the experience provided by users. _부분적으로 실시간 데이터가 반영이 안되는 경우?_
4. System continuance: the most desirable failure model for a NVE because it allows NVE execution to continue without interruption.

# Scalability
the number of entities that may simultaneously participate in the system.
A NVE entity is a participating object that is separately modeled by the participating hosts.
scalability depends on a variety of factors,including network capacity, processor capabilities, rendering speeds, and the speed and throughput of shared servers

### Conclusion
Developing effective net-VEs involves managing the interactions among a variety of system components-including the network, processor, graphics display,user input devices, databases, and other external information servers.
At the same time, the developer must support the desirable goals of heterogeneity, scalability, fault-tolerance, and easy deployability.
As an engineered system, a net-VE cannot fully achieve all of these goals simultaneously.
The designer must therefore determine which of these attributes takes priority in the net-VE implementation.
