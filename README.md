# SBWire
Modified Arduino Wire library which implements basic timeout using loop counting. The default timeout is
approximately 100 us and is calculated using F_CPU.

This library has been tested by holding SDA high, which blocks the standard `Wire` library, while `SBWire`
timesout and continues execution. When SDA is restored, I2C communication is not established until the slave
is rebooted.

# Usage
Simply replace

    #include <Wire.h>
    
With

    #include <SBWire.h>
    
The API is exactly the same.

There is a basic C function to controlling the loop count, `twi_setMaxLoops(uint16_t maxloops)`.

# Timeout Behaviour
On timeout, `twi_stop()` is called followed by `twi_init()` in an attempt to restart the bus.
