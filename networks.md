# Networks 

## Terms 
**Interface**: kernel level abstraction of NIC and Phy. 
**Host**: box with an interface (phone, computer, etc)
**Endianness** (big/little): order of bytes in a word. least significant byte first is little endian, most significant byte first is big endian. Bytes sent over the network are always big endian.


## Physical Layer
- Typing of the data is baked into the protocol, rather than the message. 

**Responsibilities:** Translate input into electrical signals, and vice versa.
- Medium is needed on which to transmit the signal.
- Switchboard is needed to route the signal to the correct destination.
- The patch panel paradigm created a circuit based network that is not scalable.
- 