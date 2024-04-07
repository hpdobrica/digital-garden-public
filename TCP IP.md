---
title: TCP IP
notetype: feed
date: 07-04-2024
---

## IP 

IP is a protocol for communication using packets to transmit data. 

Each IP packet consists of header and data. Packets sent are not guaranteed to arrive in the same order, or to arrive at all - so IP is a best-effort protocol.

## TCP

TCP is a secure protocol on top of IP, created to address its limitations.

Main difference between them is that TCP offers reliable, in-order delivery of packets. These guarantees are provided by asking the receiver to confirm the delivery of packets, and redelivers those that are lost.

The order is enforced by each packet having a sequence number, which allows receiver to reorder packets and wait for missing packets to be re-transmitted.

### TCP Connections

TCP is a connection-oriented protocol, meaning that connection must be established before communication is possible. When two programs connect to each other, one takes the role of a server (waits for connections), and other the role of a client (initiates connections). Once connection is established, the protocol is bi-directional, so both client and server can send and receive data.

Every connection is identified by destination port and IP, as well as source port and IP.
For example, when connecting to a website, web server's IP and por 443 are destination ip and port, while source ip and port are your computer's IP and a random free port. If you open a website in another tab, new connection is formed which just has a different random source port.

#### TCP Hanshake

TCP Hanshake is a 3-step process for establishing tcp connection, which ensures that connection is reliable, both sides are ready, and initial sequence numbers are established. 

First step is client initiating the connection by sending SYN (synchronize) packets to the sever, indicating that it want's to establish connection. These packets also contain sequence numbers to maintain the order of the packets.

When server receives SYN, it responds with SYN-ACK packet.

Once client receives SYN-ACK, it responds to server with ACK, and when server receives it, the connection is established.





-----

Status: #🌱 

