# D2RG_MMDVM_HS_ambe_uart_service

D2RG MMDVM HS AMBE Raspberry Pi (RPi) HAT uses NXP SC16IS752 as a SPI-UART converter to extend the number of UART ports, an MMDVM HS is then connected to SC16IS752 UART A, UART B is unused but can be used as a general purposed UART, and it is on the left (upper left corner) of the MMDVM HS AMBE HAT board.

Device Tree [RPi, assume you have the latest Raspbian running]:

<b>sc16is752-spi0-ce0.dts</b> is for SC16IS752 via RPi SPI 0 with CE/CS=0 (GPIO08) - MMDVM HS AMBE hardware configuration. 

The .dts file needs to be compiled as .dtb and put to /boot/overlays (SD Card)

```console
dtc -@ -I dts -O dtb -o sc16is752-spi0-ce0.dtb sc16is752-spi0-ce0.dts
```
And adding:
```console
dtoverlay=sc16is752-spi0-ce0
```
to config.txt under /boot (SD Card)

Then allocate serial UART interfaces to `/dev/ttySC0` and `/dev/ttySC1` - A and B, in RPi.

Under Pi-Star terminal:

```console
sudo rpi-rw

sudo su

curl -OL https://raw.githubusercontent.com/bg3mdo/D2RG_MMDVM_HS_ambe_uart_service/master/sc16is752-spi0-ce0.dts

dtc -@ -I dts -O dtb -o sc16is752-spi0-ce0.dtb sc16is752-spi0-ce0.dts

sudo mv sc16is752-spi0-ce0.dtb /boot/overlays

sudo echo "dtoverlay=sc16is752-spi0-ce0" >> /boot/config.txt
```
