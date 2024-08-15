EVAL-ADXL355-PMDZ User Guide
############################

Overview
========

The :adi:`ADXL355 <adxl355>` is a low noise density, low 0g offset drift, low power, 3-axis MEMS accelerometer with selectable measurement ranges. The ADXL355 supports the ±2g, ±4g, and ±8g ranges, and offers industry leading noise, offset drift over temperature, and long term stability, enabling precision applications with minimal calibration and with very low power consumption. Applications include:

-  Inertial measurement units (IMUs)/altitude and heading reference systems (AHRS)
-  Platform stabilization systems
-  Structural health monitoring
-  Seismic imaging
-  Tilt sensing
-  Robotics
-  Condition monitoring

The ADXL355 accelerometers offer guaranteed temperature stability with null offset coefficients of 0.15mg/°C (max). The stability minimizes resource and expense associated with calibration and testing effort, helping to achieve higher throughput for device OEMs. In addition, the hermetic package helps ensure that the end product conforms to its repeatability and stability specifications long after they leave the factory.

With output of ±2g to ±8g full scale range (FSR), selectable digital filtering from 1 Hz to 1 kHz, and low noise density of 25µ/√Hz at less than 200µA current consumption, ADXL355 MEMS accelerometer offers performance level comparable to much more expensive devices with less power consumption and BOM cost. For general board details and to buy a board, please visit the :adi:`EVAL-ADXL355-PMDZ <eval-adxl355-pmdz>` product page.

|adxl355_pmdz.png|

Input and Output Connections and Configurations
===============================================

The PMOD board is small in size with dimensions approximately 2.5 cm in width by 2.5 cm in length.

Host Processor Connector
------------------------

The PMOD interface is a series of standardized digital interfaces for various digital communication protocols such as SPI, I2C, and UART. These interface types were standardized by Digilent, which is now a division of National Instruments. Complete details on the PMOD specification can be found `here <https://www.digilentinc.com/Pmods/Digilent-Pmod_%20Interface_Specification.pdf>`__.

The specific interface used for the EVAL-ADXL355-PMDZ boards is the extended SPI. In general ADI has adopted the extended SPI connector for all PMOD devices which have an SPI interface. It provides flexibility to add interrupts, general purpose I/O, resets, and other important digitally controlled functions.

+---------------+---------------------+----------+---------------+----------------+----------+
| P1 Pin Number | Pin Function        | Mnemonic | P1 Pin Number | Pin Function   | Mnemonic |
+===============+=====================+==========+===============+================+==========+
| Pin 1         | Chip Select         | CS       | Pin 7         | Interrupt 1    | INT1     |
+---------------+---------------------+----------+---------------+----------------+----------+
| Pin 2         | Master Out Slave In | MOSI     | Pin 8         | Not Connected  | NC       |
+---------------+---------------------+----------+---------------+----------------+----------+
| Pin 3         | Master In Slave Out | MISO     | Pin 9         | Interrupt 2    | INT2     |
+---------------+---------------------+----------+---------------+----------------+----------+
| Pin 4         | Serial Clock        | SCLK     | Pin 10        | Data Ready     | DRDY     |
+---------------+---------------------+----------+---------------+----------------+----------+
| Pin 5         | Digital Ground      | DGND     | Pin 11        | Digital Ground | DGND     |
+---------------+---------------------+----------+---------------+----------------+----------+
| Pin 6         | Digital Power       | VDD      | Pin 12        | Digital Power  | VDD      |
+---------------+---------------------+----------+---------------+----------------+----------+

| 
| |adxl355_layout.png|

ADXL355 Interrupt Pins
----------------------

The EVAL-ADXL355-PMDZ has two interrupt pins and a data ready pin which can be used as external indicators for the user. The interrupt pins can be programmed through software to reflect various status flags within the ADXL355, and those pins are accessible through the SPI PMOD header. For complete details on the individual status flags, what they mean, and how to program the chip to reflect those interrupts, please consult the `ADXL355 <ADI>ADXL355>`__ data sheet.

Power Supply Considerations and Configuration
---------------------------------------------

When using the ADXL355 PMOD board, the 3.3V power for the PMOD comes directly from the host board it is connected to. The power from the host is generally capable of providing up to 100 mA at 3.3V; but for complete PMOD power specifications, please click `here <https://www.digilentinc.com/Pmods/Digilent-Pmod_%20Interface_Specification.pdf>`__.

Device Driver Support
=====================

There are two device driver solutions that are provided for controlling the **EVAL-ADXL355-PMDZ**:

   - **ADXL355 no-OS Driver**


       * The **[[ :resources:tools-software:uc-drivers:adxl355|ADXL355 no-OS driver]]** is used in bare-metal applications, typically running on low-power, embedded microcontrollers. 
       * The **[[ :resources:eval:user-guides:eval-adxl355-pmdz:no-os-setup|ADXL355 no-OS Example Project]]** uses the ADXL355 no-OS driver and has several configuration options.
         * The tinyiiod configuration emulates the Linux IIO framework through the [[repo>libtinyiiod|tinyiiod daemon library]]. The application communicates with the host computer via the serial backend, over a USB-UART physical connection. This facilitates rapid application development on a host computer, independent from embedded code development. This is the configuration that will be referenced in the no-OS platform setups below.
   - **ADXL355 Linux Driver**
       * The **[[ :resources:tools-software:linux-drivers:iio-accelerometer:adxl355|ADXL355 Linux driver]]** is used in applications running the Linux operating system, typically on larger processors and SoC devices.
       * The ADXL355 Linux driver uses the Industrial Input/Output (IIO) framework, greatly simplifying the development of application code via the cross-platform Libiio library, which is written in C and includes bindings for Python, MATLAB, C#, and other languages. Application code can run directly on the platform board, communicating with the device over the local backend, or from a remote host over the network or USB backends.\\

System Setup Using ADICUP3029
=============================

The \*\* EVAL-ADXL355-PMDZ \*\* can be used with :adi:`ADICUP3029 <eval-adicup3029>`.

Demo Requirements
-----------------

The following is the list of items needed in order to replicate this demo.

-  \*\* Hardware \*\*

   -  `EVAL-ADICUP3029 <ADI>EVAL-ADICUP3029>`__
   -  `EVAL-ADXL355-PMDZ <ADI>EVAL-ADXL355-PMDZ>`__
   -  Micro-USB to USB Cable
   -  PC or Laptop with USB Port

-  \*\* Software \*\*

   -  `ADuCM3029_demo_ADXL355.hex <repo>no-OS/releases/download/Latest/eval-adxl355-pmdz.zip>`__

.. TIP::
   
   There are two basic ways to program the ADICUP3029 with the software for the ADXL355.

   #. Dragging and Dropping the .Hex to the Daplink drive

   #. Using the drag and drop method, the software is going to be a version that Analog Devices creates for testing and evaluation purposes. This is the **EASIEST** way to get started with the reference design.

   #. Building, Compiling, and Debugging using CCES

      #. Importing the project into :adi:`CrossCore Embedded Studio <en/design-center/evaluation-hardware-and-software/software/adswt-cces.html>` is going to allow you to change parameters and customize the software to your application, but will be a bit more advanced and will require you to download the CrossCore toolchain.

.. ADMONITION:: Download

   A zip file containing prebuilt programming files for the no-OS platforms below are available at: `eval-adxl355-pmdz.zip <https://github.com/analogdevicesinc/no-OS/releases/download/last_commit/eval-adxl355-pmdz.zip>`__.

   Each platorm will typically have:
   
      - A "dummy" programming file, which implements a simple command-line program that can be run on a terminal.
      - An "iio" programming file, which allows the use of standard development tools and the libiio cross-platform library and language bindings.

   More details are provided in the platform-specific sections below.



Setting up the Hardware
-----------------------

1. Connect **EVAL-ADXL355-PMDZ** board at connector **P9** of the **EVAL-ADICUP3029**.

2. Connect a micro-USB cable to the P10 connector of the EVAL-ADICUP3029 and connect it to a computer. The final setup should look similar to the picture below. |adxl355_adicup3029_connections.jpg| <wrap center 22%> *<fc>Figure 5. Hardware Setup</fc>* </wrap>

3. Make sure the following switches are as shown from the table below. |switch_config.png| <wrap center 30%> *<fc>Figure 6. Switch Confuguration</fc>* </wrap>

4. From your PC, open My Computer and look for the DAPLINK drive, if you see this then the drivers are complete and correct. |image1| <wrap center 20%> *<fc>Figure 7. DAPLINK Drive</fc>* </wrap>

3. Drag and drop the eval-adxl355-pmdz_aducm3029_iio_example.hex file to the DAPLINK drive and your ADICUP3029 board will be programmed. The DS2 (red) LED will blink rapidly.

4. The DS2 will stop blinking and will stay ON once the programming is done.

5. For demo purposes, place the board horizontally such that the Z-axis reading will be approximately 9.8 m/s^2.


System Setup Using MAX32655FTHR or MAX32650FTHR
===============================================

The \*\* EVAL-ADXL355-PMDZ \*\* can be used with the MAX32655FTHR or MAX32650FTHR.

.. _demo-requirements-1:

Demo Requirements
-----------------

The following is the list of items needed in order to replicate this demo.

-  \*\* Hardware \*\*

   -  :adi:`MAX32655FTHR <MAX32655FTHR>` or :adi:`MAX32650FTHR <MAX32650FTHR>` with :adi:`MAX32625PICO <MAX32625PICO>`
   -  :adi:`FTHR-PMD-INTZ <FTHR-PMD-INTZ>`
   -  :adi:`EVAL-ADXL355-PMDZ <EVAL-ADXL355-PMDZ>`
   -  Micro-USB to USB Cable
   -  10-pin ribbon cable
   -  PC or Laptop with USB Port

-  \*\* Software \*\*

   -  For MAX32655FTHR,
      * Pre-built hex file: [[repo>no-OS/releases/download/Latest/eval-adxl355-pmdz.zip | MAX32655FTHR_demo_ADXL355.hex]]
      * PuTTY or other similar software
   - For MAX32650FTHR, 
      * Maxim Micros SDK [[maxim>en/design/software-description.html/swpart=SFW0010820A]]
      * Pre-built hex file: MAX32650FTHR_demo_ADXL355.hex from eval-adxl355-pmdz.zip file
      * PuTTY or other similar software

MAX32655FTHR
------------

1. Connect **MAX32655FTHR** with the **FTHR-PMOD-INTZ**. Note that MAXIM feather board should have stacking headers for feather board where the interposer board will be connected.

2. Connect \*\* EVAL-ADXL355-PMDZ \*\* to the \*\* FTHR-PMOD-INTZ \*\*.

3. Power up the **MAX32655FTHR** by connecting it to your laptop using micro-USB

4. Open the file explorer. Drag-and-drop the pre-built hex file to the DAPLINK. If the transfer was not completed, update the firmware for the DAPLINK. Follow the steps here: https://github.com/MaximIntegrated/max32625pico-firmware-images/

5. Open PuTTY or other similar software. Check the Device Manager to set correct COM for the MAX32655FTHR. Set baud rate according to hex file used:

+------------------------------------------------------------------+-----------+
| Hex file                                                         | Baud rate |
+==================================================================+===========+
| eval-adxl355-pmdz_maxim_dummy_example_max32655_adxl355           | 57600     |
+------------------------------------------------------------------+-----------+
| eval-adxl355-pmdz_maxim_iio_example_max32655_adxl355             | 115200    |
+------------------------------------------------------------------+-----------+
| eval-adxl355-pmdz_maxim_iio_trigger_example_max32655_adxl355.hex | 115200    |
+------------------------------------------------------------------+-----------+

The final setup should look similar to the picture below. |adxl355_max32655fthr_connections.jpg|

MAX32650FTHR
------------

1. Using a 10-pin ribbon cable, connect the **MAX32625PICO** to the **MAX32650FTHR**. |max32650fthr_with_pico.png| 2. Connect **MAX32650FTHR** to the **FTHR-PMOD-INTZ**.

3. Connect \*\* EVAL-ADXL355-PMDZ \*\* to the \*\* FTHR-PMOD-INTZ \*\*.

===================== ==================
MAX31855PMB1          FTHR-PMOD-INTZ SPI
===================== ==================
Pin 1 (Chip Enable)   CS
Pin 2 (Not connected) MOSI
Pin 3 (MISO)          MISO
Pin 4 (SCK)           SCK
Pin 5 (GND)           GND
Pin 6 (VCC)           VCC
===================== ==================

The final setup should look similar as shown below. |max32650fthr_adxl355pmod.jpg|

4. Power up the **MAX32650FTHR** by connecting it to your laptop using micro-USB. Connect **MAX32625PICO** to your laptop as well.

5. Open the file explorer. Drag-and-drop the pre-built hex file to the DAPLINK. If the transfer was not completed, update the firmware for the DAPLINK. Follow the steps here: https://github.com/MaximIntegrated/max32625pico-firmware-images/

6. Open PuTTY or other similar software. Check the Device Manager to set the correct COM port for the **MAX32650FTHR**.

7. Set baud rate according to the hex file used available in `MAX32650FTHR_demo_ADXL355.hex <repo>no-OS/releases/download/Latest/eval-adxl355-pmdz.zip>`__:

====================================================== =========
Hex file                                               Baud rate
====================================================== =========
eval-adxl355-pmdz_maxim_dummy_example_max32650_adxl355 57600
eval-adxl355-pmdz_maxim_iio_example_max32650_adxl355   115200
====================================================== =========

The expected output viewed in the PuTTY is shown below.

|basic_putty_adxl355.png|

System Setup Using Raspberry Pi
===============================

The \*\* EVAL-ADXL355-PMDZ \*\* can be used with a Raspberry Pi.

.. _demo-requirements-2:

Demo Requirements
-----------------

The following is a list of items needed in order to replicate this demo.

-  **Hardware**

   -  :adi:`EVAL-ADXL355-PMDZ <ADXL355>`
   -  :adi:`PMOD to Raspberry Pi Adapter (PMD-RPI-INTZ) <PMD-RPI-INTZ>`
   -  Raspberry PI Zero, Zero W, 3B+, or 4
   -  16GB (or larger) Class 10 (or faster) micro-SD card
   -  5Vdc, 2.5A power supply with micro USB connector (USB-C power supply for Raspberry Pi 4)
   -  User interface setup (choose one):

      -  HDMI monitor, keyboard, mouse plugged directly into Raspberry Pi
      -  Host Windows/Linux/Mac computer on the same network as Raspberry Pi

-  **Software**

   -  `Kuiper Linux Image </resources/tools-software/linux-software/kuiper-linux>`__

Loading Image on SD Card
------------------------

In order to boot the Raspberry Pi and control the **EVAL-ADXL355-PMDZ**, you will need to install ADI Kuiper Linux on an SD card. Complete instructions, including where to download the SD card image, how to write it to the SD card, and how to configure the system are provided on the :dokuwiki:`Kuiper Linux page </resources/tools-software/linux-software/kuiper-linux>`.

Configuring the SD Card
-----------------------

Follow the configuration procedure under **Configuring the SD Card for Raspberry Pi Projects** on the `Kuiper Linux </resources/tools-software/linux-software/kuiper-linux>`__ page, substituting the following lines in **config.txt**:

::

   dtoverlay=rpi-adxl355

.. _setting-up-the-hardware-1:

Setting up the Hardware
-----------------------

To set up the circuit for evaluation, consider the following steps:

#. Connect the **P9** of the **PMOD to Raspberry Pi Interposer** board at the male header GPIO pin connector of the **Raspberry Pi** as shown below. |image2|
#. Connect the \*\* :adi:`EVAL-ADXL355-PMDZ <EVAL-ADXL355-PMDZ>` \*\* on the PMOD to Raspberry Pi Interposer board either via Port P1 or P2. |image3|
#. Burn the SD card with the proper ADI Kuiper Linux image. Insert the burned SD card on the designated slot on the RPi.
#. Connect the system to a monitor using an HDMI cable through the mini HDMI connector on the RPi.
#. Connect a USB keyboard and mouse to the RPi through the USB ports.
#. Power on the RPi board by plugging in a 5V power supply with a micro-USB connector. The final setup should look similar to the picture below. |eval-adxl355-pmdz_overall_setup.png|

System Setup Using EVAL-ADICUP360
---------------------------------

The original software example for the ADXL355 was developed on the ADICUP360 platform, and is a simple, terminal-based command line interface. This type of example program is being deprecated in favor of tinyiiod-based servers for embedded platforms, however this example is still available for reference here: `ADXL355 Accelerometer PMOD Demo on ADICUP360 </resources/eval/user-guides/eval-adicup360/reference_designs/demo_adxl355>`__.

.. IMPORTANT::
   In order to use the **EVAL-ADXL355-PMDZ** with the **ADICUP360**, the user **MUST** remove resistor R1. The ADXL355 holds the DATA_RDY pin low during powerup, and that holds the EVAL-ADICUP360 in UART boot mode. When this mode is active the MCU will stay in standby mode till it receives the proper command, effectively making the ADuCM360 not run. So to avoid this, please remove R1 and note that you can't use the DATA_RDY pin with the ADICUP360.

.. NOTE::
   Note that the libiio, iio oscilloscope, and pyadi-iio sections below do NOT apply to this example.
   
| ===== Application Software (All Platforms) =====

Hardware Connection
~~~~~~~~~~~~~~~~~~~

The Libiio is a library used for interfacing with IIO devices and is required to be installed on your computer.

.. ADMONITION:: Download

   Download and install the latest `Libiio package <https://github.com/analogdevicesinc/libiio/releases>`__ on your machine.


To be able to connect your device, the software must be able to create a context. The context creation in the software depends on the backend used to connect to the device as well as the platform where the EVAL-ADXL355-PMDZ is attached. Two platforms are currently supported for the EVAL-ADXL355-PMDZ: Raspberry Pi using the ADI Kuiper Linux and the ADICUP3029 running the no-OS ADXL355 demo project. The user needs to supply a **URI** which will be used in the context creation.

The `iio_info </resources/tools-software/linux-software/libiio/iio_info>`__ command is a part of the libIIO package that reports all IIO attributes.

| Upon installation, simply enter the command on the terminal command line to access it.

For RPI Direct Local Access:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

   iio_info

For Windows machine connected to Raspberry Pi:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

   iio_info -u ip:<ip address of your ip>

Example:

::

       * If your Raspberry Pi has the IP address 192.168.1.7, you have to use //iio_info -u ip::192.168.1.7// as your URI

.. NOTE::
   Do note that the Windows machine and the RPI board should be connected to the same network in order for the machine to detect the device.

For Windows machine connected to ADICUP3029:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

   iio_info -u serial:<serial port>

Examples:

::

       * In a Windows machine, you can check the port of your ADICUP3029 via Device Manager in the Ports (COM & LPT) section. If your device is in COM4, you have to use //iio_info -u serial:COM4// as your URI.
       * In a Unix-based machine, you will see it under the /dev/ directory in this format "ttyUSBn", where n is a number depending on how many serial USB devices attached. If you see that your device is ttyUSB0, you have to use serial:/dev/ttyUSB0 as your URI.

IIO Commands
~~~~~~~~~~~~

There are different commands that can be used to manage and control the device being used. The `iio_attr </resources/tools-software/linux-software/libiio/iio_attr>`__ command reads and writes IIO attributes.

::

   analog@analog:~$ iio_attr [OPTION]...

Example:

::

       * To look at the context attributes, enter this code on the terminal:

::

   analog@analog:~$ iio_attr -a -C

| 
| The `iio_reg </resources/tools-software/linux-software/libiio/iio_reg>`__ command reads or writes SPI or I2C registers in an IIO device. This is generally not needed for end applications, but can be useful in debugging drivers. Note that you need to specify a context using the *-u* qualifier when you are not directly accessing the device via RPI or when you are using the ADICUP3029 platform.

::

   analog@analog:~$ iio_reg -u <context> <device> <register> [<value>]

Example:

::

       * To read the device ID (register = 0x02) of an ADXL355 interfaced via RPI from a Windows machine, enter the following code on the terminal:

::

   iio_reg -u ip:<ip address> adxl355 0x02

| 

IIO Oscilloscope
~~~~~~~~~~~~~~~~

<note important>Make sure to download/update to the latest version of IIO Oscilloscope found on this link\ https://github.com/analogdevicesinc/iio-oscilloscope/releases\ </note>

#. Once done with the installation or an update of the latest IIO Oscilloscope, open the application. The user needs to supply a URI which will be used in the context creation of the IIO Oscilloscope and the instructions can be seen from the previous section.
#. Press refresh to display available IIO Devices, once ADXL355 appeared, press connect.

|adxl355_iio_osc.png|

Debug Panel
^^^^^^^^^^^

Below is the Debug panel of ADXL355 wherein you can directly access the attributes of the device. |adxl355_iio_debug.png|

DMM Panel
^^^^^^^^^

Access the DMM panel to see the instantaneous reading of the x, y and z axis acceleration readings and the device temperature. |adxl355_iio_dmm_panel.png|

PyADI-IIO
~~~~~~~~~

| `PyADI-IIO </resources/tools-software/linux-software/pyadi-iio>`__ is a python abstraction module for ADI hardware with IIO drivers to make them easier to use. This module provides device-specific APIs built on top of the current libIIO python bindings. These interfaces try to match the driver naming as much as possible without the need to understand the complexities of libIIO and IIO.
| Follow the step-by-step procedure on how to install, configure, and set up PYADI-IIO and install the necessary packages/modules needed by referring to this `link </resources/tools-software/linux-software/pyadi-iio>`__.

Running the example
^^^^^^^^^^^^^^^^^^^

After installing and configuring PYADI-IIO in your machine, you are now ready to run python script examples. In our case, run the **adxl355_example.py** found in the examples folder.

For RPi
^^^^^^^

::

   D:\\pyadi-iio\\examples>python adxl355_example.py

Press enter and you will get these readings. |adxl355_python_example_rpi.png|

.. NOTE::
   Github link for the python sample script: `ADXL355 Python Example <https://github.com/analogdevicesinc/pyadi-iio/blob/master/examples/adxl355_example.py>`__


For No-OS
^^^^^^^^^

::

   D:\\pyadi-iio\\examples>python adxl355_no_os_example.py serial:<serial port>,57600

In a Windows machine, you can check the port of your MAX32655FTHR and MAX32650FTHR via Device Manager in the Ports (COM & LPT) section. If your device is in COM8, you have to use:

::

   python pyadi-iio/examples/adxl355_no_os_example.py serial:COM8,57600

Press enter and you will get these readings.

|no_os_adxl355_pyadi.png|

.. ADMONITION:: Download

   Github link for the python sample script: `ADXL355 Python Example <https://github.com/analogdevicesinc/pyadi-iio/blob/master/examples/adxl355_no_os_example.py>`__

More information and useful links
---------------------------------

-  :adi:`EVAL-ADXL355-PMDZ Product Page <EVAL-ADXL355-PMDZ>`
-  :adi:`ADXL355 Product Page <ADXL355>`
-  `EVAL-ADXL355-PMDZ no-OS projects <https://github.com/analogdevicesinc/no-OS/tree/master/projects/eval-adxl355-pmdz>`__

Schematic, PCB Layout, Bill of Materials
----------------------------------------

.. ADMONITION:: Download

   :adi:`EVAL-ADXL355-PMDZ Design & Integration Files <media/en/evaluation-documentation/evaluation-design-files/eval-adxl355-pmdz-designsupport.zip>`

   -  Schematics
   -  Bill of Materials
   -  Gerber Files
   -  Assembly Files
   -  Allegro Layout File


Additional Information
----------------------

-  `pyADI-IIO <https://github.com/analogdevicesinc/pyadi-iio>`__
-  `PyADI-IIO Installation Guide </resources/tools-software/linux-software/pyadi-iio>`__
-  `IIO Oscilloscope Installation Guide </resources/tools-software/linux-software/iio_oscilloscope>`__
-  `Kuiper Linux </resources/tools-software/linux-software/kuiper-linux>`__

Hardware Registration
---------------------

.. NOTE::
   Tip:
   Receive software update notifications, documentation updates, view the latest videos, and more when you register your hardware. `Register <reg>EVAL-ADXL355-PMDZ?&v=Rev B>`__ to receive all these great benefits and more!

.. |adxl355_pmdz.png| image:: adxl355_pmdz.png
   :width: 350px
.. |adxl355_layout.png| image:: adxl355_layout.png
   :width: 300px
.. |adxl355_adicup3029_connections.jpg| image:: adxl355_adicup3029_connections.jpg
   :width: 900px
.. |switch_config.png| image:: switch_config.png
   :width: 900px
.. |image1| image:: daplink.jpg
   :width: 300px
.. |adxl355_max32655fthr_connections.jpg| image:: adxl355_max32655fthr_connections.jpg
   :width: 450px
.. |max32650fthr_with_pico.png| image:: max32650fthr_with_pico.png
   :width: 400px
.. |max32650fthr_adxl355pmod.jpg| image:: max32650fthr_adxl355pmod.jpg
   :width: 450px
.. |basic_putty_adxl355.png| image:: basic_putty_adxl355.png
   :width: 600px
.. |image2| image:: interposer.png
   :width: 500px
.. |image3| image:: adxl355_rpi_connections.jpg
   :width: 600px
.. |eval-adxl355-pmdz_overall_setup.png| image:: eval-adxl355-pmdz_overall_setup.png
   :width: 600px
.. |adxl355_iio_osc.png| image:: adxl355_iio_osc.png
   :width: 300px
.. |adxl355_iio_debug.png| image:: adxl355_iio_debug.png
   :width: 400px
.. |adxl355_iio_dmm_panel.png| image:: adxl355_iio_dmm_panel.png
   :width: 400px
.. |adxl355_python_example_rpi.png| image:: adxl355_python_example_rpi.png
   :width: 600px
.. |no_os_adxl355_pyadi.png| image:: no_os_adxl355_pyadi.png
   :width: 600px