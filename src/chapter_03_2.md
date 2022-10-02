## 1553 System Architecture

#### Key Elements of 1553 Archietecture

* BC (BUS controller)
* Bus monitor
* RT
* Stand-alon remote terminal
* Twisted pair shielded cable


### BUS CONTROLLER (BC)

The BC provides data flow control for all transmissino on the bus. It has the ability to send as well as recieve data. It is the only unit on the bus that initates a transmission. The BUS Controller uses a command reponse method of data transfer. No other device can talk on the bus unless ordered by the BC. 

### Bus Monitor
A bus monitor is a passive unit on the bus. The 1553-standard defines a bus monitor as a "terminal assigned the task of receiving bus traffic and extracing selected information to be used at a later time" 

#### Bus Analyzer

THe first type of monitor is called the bus analyzer. These systems are used extensively in software support facilities and integration labs and can be very helpful to the flight tester. Examining a weapons release sequence shows an example of ho this device can be use. 

##### Weapon Release Example

| Time      | Event |
| ----------- | ----------- |
| 0      | Trigger Depress    |
| 10 msecs  | Battery Arm     |
| 35 msecs  | Rocket Motor Arm      |
| 50 msecs   | Ejector arm       |
| 150 msecs   | Roll command sent     |
| 200 msecs   | frequency set        |
| 350 msecs  | Ejector fire     |
| 500 msecs   | Rocket motor fire    |


###  Remote Terminal
THe RT may be thought of as the avionic component or sensor connected to the bus. An inertial navigation system (INS), global navigation satellite system (GNSS), radar display processor, or electo-optical senosr can be used as RTs. 

#### non-1553 systems

* Digital converter
* signal interface unit
* center air data computer (CADC)
* TACAN
* radar altimeter
* ILS 
* fuel quantity

## Command Words

The command word is sent by the Bus Controller. 

Features of a command word:

* 3-bit time synchronization pattern
* 5-bit RT address
* 1-bit transmit/recieve
* 5-bit subaddress/mode field
* 5-bit word count/mode code field
* 1-bit parity check.
* Total of 20 bits

The 1553 terminal add the synchronization and parity before transmission and remove them from reception.  Therefore the nominal word size is 16 bits. 

Lets look at an example. If the BC wants to get nine-state vecto inofrmation from the INS, the bus controller will start by initaing a command word. Lets look at information on the INS to figure out how we would contruct this command word. The INS is indentified at RT 12 on this particular bus. The first 5 bits (after the 3-bit synchronization is removed) of the command word are used to identify the RT address. 

Because the address is determined by 5 bits, we can only have 31 RTs on the bus. There 32 possible combinations for 5 bit word, but if we do not include the bit (0), which we do not, we only have 31 possible combinations. When this command word is sent onto the bus, the INS will read it, but all other remote terminals will ignore it. 

The next bit is the transmit and recieve bit. As may guess, this bit is meant to determine if the bus controller is requesting or sending data to the INS. When requesting data this bit is set to a "1". When sending data to the RT, this is set to "0".

The next 5-bit field is the subaddress/mode and the final 5-bits comprise the word count/mode code field. These final 5 bits determine how many data words are to be sent or received. If each of the nine-state vector parameters required one data word, then the word count would be nine. THe INS either measures or computess latitude, longitude, altitude, velocities (north, east, and down [NED]), accelerations (NED), heading, ground track, groundspeed, ptich, rool, yaw , time-to-go, distance-to-go, cross track ang along track errors, and monay other paramters. The 5-bit subaddress fiedl has around 32 associated data words. There are two reserve fields: 00000 and 11111 that are used for mode commands. 




