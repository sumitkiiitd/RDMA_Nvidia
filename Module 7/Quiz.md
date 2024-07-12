### Question 1
**RDMA vs Socket Programming**
Which of the following statements are true (select 2):

- [ ] RDMA cannot coexist with socket programming on the same application.
- [x] Socket programming relies on system calls which uses the OS API.
- [x] With RDMA, the operating system API is used directly with the dedicated hardware, which makes data-transfer faster.
- [ ] RDMA provides better latency and utilization of the hosting machine hardware.

### Question 2
**RDMA and bypassing the OS**
Which of the following statements are true (select 2):

- [x] In RDMA, data is passed directly to the dedicated hardware (e.g., NVIDIA Adapter) without involving the OS.
- [ ] OS is not involved while using RDMA, and does not require any software to be installed on the host OS (e.g., device driver).
- [ ] RDMA can be used on any machine, as long as it is running a LINUX based OS.
- [x] There are RDMA operations that go through the operating system.

### Question 3
**RDMA and bypassing the OS**
Which of the following statements are true (select 2):

- [ ] RDMA programming library is using the same API as the traditional socket API (e.g., connect(), bind(), listen(), accept()).
- [ ] When sending or receiving data, RDMA is using the socket library to pass the data to the device driver, from which it is being sent to the dedicated hardware.
- [x] RDMA control operations such as resource allocation or connection establishment typically involve the host OS.
- [x] Some RDMA operations are not involving the host OS, but there are RDMA operations that go through the OS.

### Question 4
**RDMA and Communication Models**
Select the correct answer:

- [ ] RDMA is implemented as a two-sided communication model, the sender sends information, and the receiver accepts it and stores it in its memory.
- [ ] RDMA doesn’t have to know the remote side address, it can store the information directly in the destination buffers.
- [ ] RDMA caches the data in HW buffers and sends it to the other side upon request by using system API calls.
- [x] RDMA supports the one-sided communication model, where the sender can send data but the receiver does not need to be involved.

### Question 5
**Sending Data with RDMA**
Which of the following statements are true (select 2):

- [ ] RDMA uses temporary buffers on both sides and copies data to and from those buffers.
- [x] RDMA uses the “zero-copy” method, which avoids making data copies on the destination host side.
- [ ] RDMA is extremely efficient when it comes to small messages, the smaller the message - the faster RDMA will be able to send it.
- [x] RDMA tries to minimize the number of memory copies needed to transfer the data to the destination memory.

### Question 6
**Zero Copy and RDMA**
What would be the optimal message size to be sent using RDMA?

- [ ] The message size needs to be at least half of the local memory buffer, so that RDMA can send and receive messages on the same buffer.
- [ ] RDMA uses “zero copy” which is going to save more time when dealing with large messages.
- [ ] Message size will not affect the overall performance as long as it fits the MTU configured on the physical link connecting the hosts (or host to switch).
- [x] Small messages that can fit a single buffer are ideal, which makes it easier to copy from one buffer to another with no re-allocations.

### Question 7
**RDMA Transport Layer**
Which of the following statements are true (select 2):

- [x] RDMA transport layer is responsible for determining if a connection is used for a single message or a constant flow of data.
- [ ] RDMA transport layer is responsible for determining the destination address of the remote host.
- [ ] The transport layer adds the CRC field on each InfiniBand packet, which is used to check if the packet is corrupted.
- [ ] RDMA transport layer is responsible for determining if a connection needs to be established for the data transport process.

### Question 8
**RDMA Transport Layer**
Which of the following statements are true (Select 2):

- [ ] RDMA RC transport is much more scalable than RDMA UD transport.
- [x] RDMA UD transport is a un-reliable datagram service, it can be compared to UDP in the traditional TCP/IP protocol stack.
- [ ] RDMA UD transport is typically used for client-server applications.
- [x] RDMA RC transport is a reliable connection-oriented transport, it can be compared to TCP in the traditional TCP/IP protocol stack.

### Question 9
**RDMA Transport Layer**
Which of the following are mechanisms to enforce reliability in message transport process (Reliability = making sure the entire message will arrive at the other end) (select 2):

- [x] Message numbering to decide which message part needs to be retransmitted.
- [x] Error messages (notifications) that tells the sender if it needs to retransmit the message.
- [ ] “Timeouts” to decide if a message needs to be retransmitted.
- [ ] Connection manager that queries both side of the connection and able to check that all messages are received.

### Question 10
**RDMA Verbs**
Select the correct answer:

- [x] Libibverbs is an open-source user space library for RDMA applications.
- [ ] Libibverbs is part of the Mellanox OFED driver.
- [ ] Verbs API is used as a wrapper for the Socket API.
- [ ] RDMA applications don’t have to link against Libibverbs, it can work out of the box as long as it has the right hardware connected on the host running the app.

### Question 11
**RDMA Verbs**
Which of the following are objects that are part of the verbs API (Select 3):

- [x] Buffer Queue.
- [x] Completion Queue.
- [x] Work Request.
- [ ] Work Completion.

### Question 12
**RDMA Verbs**
Which of the following statements are true (Select 2):

- [x] Work requests that are posted to Work Queues will be handled by the hardware in the order they were posted.
- [x] QP object contains two Work Queues – for sending and receiving.
- [ ] A work request buffer (that was either sent or received) can only be accessed when the work request is marked as outstanding.
- [ ] When an application wants to send data, it will post a work request to the Completion Queue and wait for it to be sent to the other side.

### Question 13
**Data Path Flow**
Assume a message or several messages were sent by an RDMA application. Which of the following steps are necessary on the receiver side to receive the messages: (Select 3):

- [ ] Create a QP for each expected message sent by the sender side.
- [x] Check for Work Completion along with the status of the operation.
- [x] Create a Work Request and post it on the Receive Queue.
- [x] Allocate buffers to store the received messages.

### Question 14
**Data Path Flow**
Assume a message or several messages were sent by an RDMA application. Which of the following steps are necessary on the sender side to send the messages: (Select 3):

- [ ] Check for Work Completion along with the status of the operation for each Work Queue entry.
- [ ] Resolve the destination app IP address and port and configure the Socket accordingly.
- [x] Post each Work Request to the Send Queue.
- [x] Generate Work Request for each message that is being sent to the other side.

### Question 15
**RDMA Memory Management**
Which of the following statements are true (Select 2):

- [x] RDMA MM (Memory Manager) is in charge of mapping the physical memory to the virtual memory of the process.
- [ ] RDMA allows the application to access any vacant address on the host memory without getting a segmentation fault.
- [x] Verbs can only send or receive to registered memory.
- [ ] RDMA memory registration involves the host OS.

### Question 16
**RDMA RC Connection**
Which of the following steps are needed to form RC connection between RDMA applications? (Select 2):

- [x] Both applications need to create a QP and make sure the other side has the QP address.
- [ ] One of the applications has to set the MTU to a value of at least 1500.
- [x] Both sides QPs need to be set with the RTS state (Ready To Send).
- [ ] The receiver side QP needs to be set with the RTR state (Ready To Receive).

### Question 17
**RDMA Programming**
Which of the following is the correct order of operations that is required to release resources for RDMA applications (Select the correct answer):

- [ ] Call `free()` to free the memory used for the buffer and the context itself.
- [ ] If a completion channel was used, `ibv_close_device` is used to destroy it.
- [x] `ibv_dereg_mr` – to deregister the memory region used for sending and receiving data.
- [x] `ibv_destroy_QP` and `ibv_destroy_CQ` - to destroy the queue pair and the completion queue respectively.

### Question 18
**RDMA Programming**
Which of the following is the correct order of operations that is required to release resources for RDMA applications (Select the correct answer):

- [x] 1.ibv_destroy_QP and ibv_destroy_CQ - to destroy the queue pair and the completion queue respectively.
      2.ibv_dereg_mr– to deregister the memory region used for sending and receiving data
      3.If a completion channel was used, ibv_close_device is used to destroy it.
      4.Call free() to free the memory used for the buffer and the context itself.



- [ ] 1.Call free() to free the memory used for the buffer and the context itself.<br>
      2.If a completion channel was used, ibv_close_device is used to destroy it.<br>
      3.ibv_dereg_mr– to deregister the memory region used for sending and receiving data.<br>
      4.ibv_destroy_QP and ibv_destroy_CQ - to destroy the queue pair and the completion queue respectively.



- [ ] 1.ibv_dereg_mr– to deregister the memory region used for sending and receiving data.<br>
      2.ibv_destroy_QP and ibv_destroy_CQ - to destroy the queue pair and the completion queue respectively.<br>
      3.Call free() to free the memory used for the buffer and the context itself.<br>
      4.If a completion channel was used, ibv_close_device is used to destroy it.

### Question 19
**RDMA Memory Management**
Which rdma Libibverbs command can be used to check the completion queue (Select the correct answer):

- [x] ibv_poll_cq
- [ ] ibv_post_receive
- [ ] ibv_check_status
- [ ] ibv_post_wr

### Question 20
**RDMA CM**
RDMA CM is used to manage connections for RDMA.
Which of the following statements are true (Select 2):

- [x] RDMA CM has an event channel to be used for connection establishment events.
- [ ] RDMA CM is part of the IB verbs library.
- [x] RDMA CM API is designed to be similar to server-client in TCP.
- [ ] RDMA CM can be used to automate the data sending and receive process for RDMA apps.
