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


## 3. Building Blocks of UDP