## 13.6 Connecting the Software-Definable Pins

               (SDPs)
The X550 has four SDPs per port that can be used for miscellaneous hardware or software-controllable
purposes. These pins and their function are bound to a specific LAN device. The pins can each be
individually configured to act as either input or output pins via Flash. The initial value in case of an
output can also be configured in the same way. However, the X550 default for any of these pins is to be
configured as outputs.
To avoid signal contention, all four pins (per port) are set as input pins until the Flash configuration has
been loaded.
Choose the correct SDPs for specific applications. All pins are tri-state buffers. Consider that four of
these pins (SDPx_0 – SDPx_3) can be used to support IEEE1588 auxiliary devices, input for external
interrupts, indication for thermal-sensor event or as general purpose interrupt (GPI) inputs. To act as
GPI pins, the desired pins must be configured as inputs. A separate GPI interrupt-detection enable is
then used to enable rising-edge detection of the input pin (rising-edge detection occurs by comparing
values sampled at 62.5 MHz, as opposed to an edge-detection circuit). When detected, a corresponding
GPI interrupt is indicated in the Interrupt Cause register.
When connecting the SDPs to different digital signals please keep in mind that these are 3.3V signals
and use level shifting if necessary.
The use, direction, and values of SDPs are controlled and accessed using fields in the Extended SDP
Control (ESDP) and Extended OD SDP Control (EODSDP) registers.
