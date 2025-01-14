# Lesson 4: GPS Coordinates

## High Altitude Balloon Data Logging

### Pre-requisites
* Complete [Lesson 1: Blinking Light](../lesson1/README.md)
* [Thonny Python IDE](https://thonny.org/) installed on your computer
* All necessary hardware components (Raspberry Pi Pico, GTU-7 module, breadboard, wires, USB cable, computer)

### Objectives
* Use breadboard to wire GTU-7 module to Raspberry Pi Pico
* Install the GTU-7 MicroPython driver to the Raspberry Pi Pico
* Print GPS coordinates to the console

### Results
* Familiarity with wiring a breadboard
* Understanding of basic MicroPython code
* Learn the importance of MicroPython drivers and how to use them
* A functioning program for reading GPS data and printing the information to the console<br><br>

### Video Walk-through
In addition to the reading below, you can watch this [video](videos/Lesson4.mp4?raw=true) for guidance!
<br><br>

## Steps

  **IMPORTANT** Before wiring your Pico, UNPLUG IT FROM YOUR COMPUTER. If plugged in while wiring, you risk damaging the Pico or GT-U7 module.

1. Wire the GT-U7 to the Raspberry Pi Pico.
    GT-U7 Pins | Description | Pi Pico Pins
    ------------ | ----------- | ------------
    VCC          | (Voltage In): Provides power. Connect to the 5V pin on Pico | 5V (40)
    GND          | (Ground): Connect to the ground pin on Pico | GND (38)
    PPS          | (Pulse Per Second): Assists with synchronization | N/A
    TXD          | (Transmit): Transmission pin used for serial communication | UART1 RX / GP5 (7)
    RXD          | (Receive): Receiver pin used for serial communication | UART1 TX / GP4 (6)

    ![gtu7-diagram](./docs/pi-pico-gtu7.png)

    ![Lesson Four](./images/WireUp.jpg)

### Install GT-U7 Driver

Drivers are code modules for enabling certain functionality. One such driver allows us to read data from the GTU-7 module. This driver is called `gtu7.py` and is located in the [../drivers/src/gtu7.py](../drivers/src/gtu7.py) location. The following steps will result in saving this driver to the Raspberry Pi Pico so the driver can be used by our Python code.

1. Download the driver called `gtu7.py` located in the [../drivers/src/gtu7.py](../drivers/src/gtu7.py) location.

1. Connect your Raspberry Pi Pico to your computer using the USB cable.

1. Open the Thonny IDE. _Stop/Restart_ the backend to refresh the connection.

    ![stop-restart](./docs/thonny-1.png)

    You should now see `Raspberry Pi Pico` displayed in the left-hand navigation of Thonny.If the "Files" window is not displaying add it from the View > Files menu.

    ![files-menu](../lesson-3/docs/FilesView.jpg)

1. If one does not already exist, create a new directory in Thonny on the Raspberry Pi Pic called `drivers`.
    
    ![drivers-directory](./docs/thonny-2.png)

1. Using Thonny, select _File_ then _Open_ from the menu. Choose _This Computer_. Navigate to the location where you downloaded `gtu7.py` in a previous step. Select the file and click _Open_.

1. Save the `gtu7.py` file to the Raspberry Pi Pico. This allows our code to use the driver to perform GT-U7 actions in MicroPython when running on the Pi Pico. 

    Click _File_ then _Save as..._. Choose _Raspberry Pi Pico_. Double-click the `drivers` folder created in a previous step. Then save the `gtu7.py` file being sure to name it `gtu7.py`.

1. If a file called `__init__.py` does not already exist in the `/drivers` folder, create a new file in Thonny called `__init__.py`. 

    Click _File_ then _New_. Then click _File_ then _Save as..._. Choose _Raspberry Pi Pico_ and save this empty file to the same `drivers` location as the previous step. Name the file `__init__.py`. This empty file is used by Python to indicate the `drivers` folder is to be used for Python modules.

    Your finished folders and files should look like this:<br>
    ![files-menu](./docs/FinishedFiles.png)

### GT-U7 Program

The steps in this section will use the previous hardware and driver sections to allow reading temperature, pressure, and altitude from the GT-U7 module. The code example for this lesson is located in [./src/main.py](./src/main.py).

1. Using Thonny, open the `main.py` file in [./src/main.py](./src/main.py).

1. Run the script.

    ![run-script](./docs/thonny-3.png)

    Output will be generated to the console in Thonny describing the actions being taken. You will see output for latitude, longitude, number of satellites, and time returned from the GPS module.

    Example output:

    ```
    Latitude: 	 4026.774
    Longitude: 	 -8902.08
    Satellites:  6
    Time:		 18:46:14
    ```

**Congratulations! You have successfully completed Lesson 4.**

<br><br>

## Want more?
If you have finished with the base lesson, check out the items below.
<br><br>

Things to think about, validate, and/or try:
* What are the units/formats of the module output? 🤔
* How accurate is the readout of the module? 
    * Coordinates?
    * Date?
    * Time?
* What other readings are available from the module? (**Hint:** look at the driver...) 😏
* What is UART and how are we using it? 😵

Update the code to do any/all of the following:
1. Add the units to the end/middle of the output
1. Print out another module data point 😁
<br><br>

## Troubleshooting

* `ERROR: No GPS data returned`

  If you are not receiving GPS data, the following may be the case:

  * You have the RX and TX connections reversed. Be sure the TX on the GT-U7 goes to the UART RX on the Pico, and the RX on the GT-U7 goes to the UART TX on the Pico.
  * Your GPS device has not yet established a connection with satellites. Be patient, this can sometimes take several minutes.
  * In some cases GPS data is returned, in other cases it is not. Expect to see some intervals fail while other succeed. Again, this is dependent on the GPS having a good connection with satellites.
  * If after several minutes you are still not receiving GPS data, ensure you are in a location where the GPS module can successfully connect. Move to a higher floor in your location, or near a window.

* `ERROR: No module named (drivers, bmp180, ...)`
    
    If you see this error it means Python is not able to locate a module to be imported. This can occur because the version of MicroPyhon you are using does not support the module you are trying to import. Specifically for this lesson it likely applies to the `drivers` step. Ensure the `drivers` folder and its contents, `gtu7.py` and `__init__.py`, are saved to the Raspberry Pi Pico device and _not_ your computer.

    Example error message:
    ```sh
    Traceback (most recent call last):
      File "<stdin>", line 2, in <module>
    ImportError: no module named 'drivers'
    ```

## Need help?
Watch the walk-through [video](videos/Lesson4.mp4?raw=true) for guidance!