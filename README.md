# None_Voltiale_Memory_Manger
simple memory manager stack

## Components:
<div style="text-align:center"><image src="nvm_hardware.png"/></div>


## Static Architecutre:
<div style="text-align:center"><image src="nvm_static_desgin.png"/></div>

## Application:
 * lcd display two button press counter c0 and c1.
 * each button counter value increased by 1 if the related button pressed.
 * in case of shutdown the value of the two counter stored in non-volitaile memory in specified logical  adresses.
 * each logical adress mapped to different EEPROM one external and the other is internal.
 * in case of power up the values are copied from both non-volitaile memory to ram mirror.
 * the values get validated throught a CRC check done by the nvm.
 * if the data is courrpted the nvm notify the application and set the mirror to default values.
 * if the data is valid the nvm copies it to ram mirror.
 * the application carries on until a power off routine is fired, all data writen back to memeory.


## Memory Stack:
 
### None-Voltile Memory Module:
 * this moudle interface with all application requests and manage them throw the memory interface module. 
 * keeps track of none-voltaile memory in ram mirror that is updated when the the system turned on and a write all data back in the shutdown rotuine.
 * perform a CRC redundancy check on the data to validate it's correctness.

### Memory Interface Module:
 * takes logical adresses and map them to pysical addresses either on external or internal E2PROM.
 * write or read data from external or internal E2PROM depend on the logical adress.
 * notify the manager when request finished through a call back.
 
### External E2PROM Module | Internal E2PROM Module.
