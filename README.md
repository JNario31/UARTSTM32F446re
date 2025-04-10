This implements the same function as the other UART repo "UARTSTM32" but in interrupt mode or non blocking mode. The reason for utilizing 
this mode is in the case there is a critical function that needs to be processed and cannot be blocked by waiting for transmission and reception
from the UART peripheral. In this case we have a function performCriticalTasks() (which does not perform any critical tasks) that needs to be processed. In order
to process these tasks we put the UART peripheral in interrupt mode so that it is no longer blocking theses tasks.

The interrupt is invoked upon user input (UartReady = SET) and UART peripheral ISR is ran.
