This service consists of a single characteristic, called **Key Press State**, which notifies the state changes of the buttons, `BTN1` and `BTN2`.

The characteristic **Key Press State** has a value attribute containing an *unsigned integer of 8 bits*.  

Each bit represents the state of a button:
* `0` is for **Released**
* `1` is for **Pressed**

This value does not have access either read or write.  
It is communicated to the client only through notifications or indications, which can be enabled via the **Characteristic Client Configuration** descriptor. 
