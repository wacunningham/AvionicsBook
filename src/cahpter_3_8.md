## Anomalous command word conditions


Suppose there was a parameter on the aircraft that all systems used in their computations. Alitude is a good example. Sensor systems, electronic warfare (EW) systems, weapon systems, and navigation system all use altitude. Since all systems use this paramter it is easier to broadcasting to every RT at the same time then to send it to each one individually. This is broadcast mode. When the RT address is set to 31 (11111), all RTs read the messsage. Unfortunately, the RTs cannot respond stating that they received the message because all of the replies would come back at the same time, making identification of repsondants impossible. Most aircraft that used MIL-STD-1553 do not emply broadcast mode. 

If the RT needs to perform a self-test, or reset, or synchronize, it must wait until commaned by the BC. These operations are called mode commands. The subaddress of 0 (00000) or 31 (11111) tells the RT that the misseage is a mode comand, and the word count is replaced with the code of the specific operation. 

## Command word Summary

The command word is a 20-bit word sent by the Bus Controller to an RT. The 3-bit synchronization and 1-bit parity are added before transmissino and removed during reception. The remaining 16 bits are comprised of

* A 5-bit field of the RT addrss; RT 31 (1111) is reserved for broadcast mode. Broadcast is not efficent and therefore not widely used. A total of 31 RTs may coccupy a bus.
* A 1-bit field  for transmit/recieve: 1 = transmit, 0 = recive
* A 5-bit field for the subaddress. The subaddress allows more data to be exchanged. A 0 (00000) or 31 (11111) in teh subaddress field indicates a mode command. The transmit/receive bit in a mode command is per the documentation
* A 5-bit field for the data word count. If a 0(00000) or 31 (11111) occupies the subaddress field, the data word count bcomes the mode code. Mode code are assigned per the documentation. 

