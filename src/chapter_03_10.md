## Status Words

After the remote terminal receives a command from the BC, it will build a status word that informt he bus controller of the Remote Terminal's status as well as the result of the last transmission. The first 5 bits are the responding RT's address. THis lets the Bus controller know which RT this status word is coming from. The next 11 bits ar ea status field. If the message is recieved without error and the RT's health and welfare are good, then the status field will filled with all 0's. 

The first bit after the RT address is the message error idenification. The receiving RT validate each word and message using the following criteria:

    * The word begins with a valid sync
    * The bits are a valid Machester II code
    * The word parity is odd
    * The message is contiguous
  

The remaining bits in the status word are called status bits. The instrumentation bit can be used to discriminate the command word from teh status word (They have the same synchronization). The logic would be 0 in the status word and 1 in the command word. 

The next bit is the service request bit is the next status in the feild and is used to indicate to the bus controller that the RT requires service. When this bit is set to 1, the BC may send command a predetermined action or request transmission of a vector word that will identify the type of service requested.

The next three bits are reserved by the DOD. 

The next bit is the broadcast commadn received status. 

The next bit is the busy bit to indicate if the RT cannot respond due to a busy condition. 

A subsystem flag inicates that a fualt exist in teh RT's subsystem and that the data required may not be readable. This should not be confused with the last status bit, called the terminal flag. The terminal flag indicates if there is a problem with RT and not its subsystem. 

A dynamic buss control acceptance bit indicates to teh bus controller that RT is ready to take control of the bus after receiving to take control mode command. In some applications, this procedure is illegal and the bit will alawys be set to 0. 

