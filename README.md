# mmdvm_hs_ambe_uart_service

MMDVM HS AMBE uses NXP SC16IS752 as a SPI to UART converter to extend the number of UART ports, a MMDVM HS is then connected to SC16IS752 UART A, UART B left unused but can be used as a generic UART, and it is on the left (left upper corner) of the MMDVM HS AMBE board.

Device Tree [RPi, assume you have the latest Raspbian running]:

sc16is752-spi0-ce0.dts is for SC16IS752 via SPI0 with CE/CS=0 (GPIO08)

The .dts file needs to be compiled as .dtb and put to /boot/overlays 

```console
dtc -@ -I dts -O dtb -o sc16is752-spi0-ce0.dtb sc16is752-spi0-ce0.dts
```
Adding :
```console
dtoverlay=sc16is752-spi0
```
to config.txt under /boot

Then allocate serial UART interfaces to `/dev/ttySC0` and `/dev/ttySC1`  - A and B
