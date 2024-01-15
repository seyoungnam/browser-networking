# Part 1. Networking 101

## 1. Primer on Latency and Bandwidth

### Latency and Bandwidth

- **Latency**: The time from the source sending a packet to the destination receiving it
- **Bandwidth**: Maximum throughput of a logical or physical communication path
    > [!NOTE]: Throughput is how much data was transferred from a source at any given time

<br>
<img src="https://d3ansictanv2wj.cloudfront.net/hpbn_0101-13f123fd47ea08d5c5dec2bd8712c833.png" alt="Latency and Bandwidth" width="600"/>
<br>

### The Many Components of Latency

- **Propagation delay**
    - Time for a message to travel from the sender to receiver
    - distance over speed ( distance / (distance/time) = time )
    - perceptible "lag" is a delay of over 100-200 milliseconds 
- **Transmission delay**
    - Time to push all the packet's bits into the link
    - a function of the packet's length and data rate of the link
        > [!NOTE]: data rate of the link is the number of bits per second
- **Processing delay**
    - Time to process the packet header, check for bit-leve errors, and determine the packet's destination
- **Queuing delay**
    - Time the incoming packet is waiting in the queue until it can be processed

### Bandwidth in Core Networks

- channel = wavelength
- bandwidth of a fiber link (70 Tbit/s) is the multiple of
    - per-channel data rate (171 Gbit/s) and
    - the number of multiplexed channels (400 wavelengths)
- 


## 2. Building Blocks of TCP

### Three-Way Handshake

<br>
<img src="https://orm-chimera-prod.s3.amazonaws.com/1230000000545/images/hpbn_0201.png" alt="three-way handshake" width="600"/>
<br>

All TCP connections begin with a three-way handshake.
- SYN
    - Client picks a random sequence number x and sends a SYN packet, which may also include additional TCP flags and options.
- SYN ACK
    - Server increments x by one, picks own random sequence number y, appends its own set of flags and options, and dispatches the response.
- ACK
    - Client increments both x and y by one and completes the handshake by dispatching the last ACK packet in the handshake.

The client can send a data packet immediately after the ACK packet, and the server must wait for the ACK before it can dispatch any data.
Each new connection will have a full roundtrip of latency before any application data can be transferred.

### Congestion Avoidance and Control

**Congestion Collapse** refers to a situation where links stays busy but transfer rates(goodput) fall as retransmissions clog the network(see "[Congestion collapse](https://www.freesoft.org/CIE/RFC/896/2.htm)").

To address this issue, multiple mechanisms were implemented in TCP: flow control, congestion control, and congestion avoidance.

#### Flow Control

Flow control is a mechanism to prevent the sender from overwhelming the receiver with data it may not be able to process -- the receiver may be busy, under heavy load, or may only be willing to allocate a fixed amount of buffer space.

Each side of the TCP connection **advertises its own receive window (rwnd)**, which communicates **the size of the available buffer space** to hold the incoming data. When the connection is first established, both sides initiate their rwnd values by using their system default settings.

Each ACK packet carries the latest rwnd value for each side, allowing both sides to dynamically adjust the data flow rate to the capacity and processing speed of the sender and receiver.

> Window Scaling(RFC 1323): 16 bits(2^16, 65,535 bytes) are the hard limit for the receive window size. RFC 1323 was drafted to provide a "TCP window scaling" option, which allows to raise the max receive window size from 65,535 bytes to 1 gigabyte. This option iscommunicated during the three-way handshake.


#### Slow-Start

The problem of flow control is that niether the sender nor the receiver knows the available bandwidth at the beginning of a new connection. If data rate is not adjusted while the number of connections increases, the data will simploy pile up at some intermediate gateway and packets will be dropped, leading to inefficient use of the network.




## 3. Building Blocks of UDP