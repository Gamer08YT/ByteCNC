# Controller

The Motion Controller is based on the 5A-75B wich is a cheap LED Driver Board.

### Why?

The Board has two 1 GBit/s NICs, has 16 HUB75-connectors, with each 6 individual pins (96 total). Besides these pins, there are 8 shared pins. This makes the total number of usable pins 104.

<img height="300px" src="https://raw.githubusercontent.com/q3k/chubby75/refs/heads/master/5a-75e/images/cl-5a-75e-v71-front.jpg"/>

Most Boards wich much GPIOs are very expensive, like Mesa or ProjectCNC.

For many beginnings, these qualitative but expensive cards are often difficult to manage.

### Idea

The idea is to desolder the 74HC245T Chips (levelshifters) and directly attach the FPGA to the connector to use some IOs as Input Pins. 

https://zeromips.org/posts/2022-05-29-5a-75b/

### Bypass PCB

You can use a flexible PCB to Bypass the 74LVC245 IC see https://github.com/Disasm/hc245t-bypass .

### Software
As Software i use LinuxCNC running on a Lenovo Thinkcenter.

To adopt the card i use following project https://github.com/Peter-van-Tol/LiteX-CNC wich simulates a Mesa Driver.

### Build && Flash

If you flash, please plugin the board first, than you can connect the JTAG Programmer to your PC.

#### ESP Programmer

https://deepwiki.com/riscv-collab/riscv-openocd/4.3.1-ftdi-based-adapters

To use the ESP Programmer to flash the FPGA you need to install the ``fpga-icestorm`` Driver.

The Connection Log can be checked with ``sudo dmesg | grep FTDI``.

You can list connected FTDI Devices via ``lsusb | grep -i ftdi``!

```
litexcnc build_firmware 5a-75b_v8.0_i24o32.json --build
litexcnc flash_firmware --programmer ftdi/esp32_devkitj_v1 colorlight_5a_75b.svf
```

#### Usage in HAL

If you have LinuxCNC installed on the machine, you can test the connection with the card and show the created pins. Start a the hal with halrun and type the following commands:
loadrt litexcnc connections="eth:10.0.0.10"
show pin
show param
show function

##### Ethernet

```loadrt litexcnc connections="eth:<IP-address>"```

##### SPI
```loadrt litexcnc connections="spidev:/dev/spidev0.0"```
or pigpio
```loadrt litexcnc connections="pigpio:<CS_channel>:<speed>"```

#### Other interface?

You can list all available interfaces via ``openocd -c interface_list`` or with ``openocd -c apdater list`` wich is currently not working for me.
