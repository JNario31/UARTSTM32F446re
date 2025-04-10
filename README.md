This implements the same function as the other UART repo "UARTSTM32" but in interrupt mode or non blocking mode. The reason for utilizing 
this mode is in the case there is a critical function that needs to be processed and cannot be blocked by waiting for transmission and reception
from the UART peripheral. In this case we have a function performCriticalTasks() (which does not perform any critical tasks) that needs to be processed. In order
to process these tasks we put the UART peripheral in interrupt mode so that it is no longer blocking theses tasks.

The interrupt is invoked upon user input (UartReady = SET) and UART peripheral ISR is ran. In interrupt mode the application does not wait for data transmission,
it waits to put data into the DR register or to load data into the application memory via the ISR.

There is a issue with this code. When transmitting the data to the serial monitor it cannot be implemented the same way in the previous example as the function calls will be faster than the UART tranmission itself. Thus we must wait for each message to finish transmitting before we transmit the next, essentially putting this part of the application back into polling, which is not good as it takes time away from our very important critical tasks.

An elegant solution is to use a temporary data structure to store the bytes and let the ISR transmit them, this will be done in the next repo :)
