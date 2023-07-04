<h2> <b>IoT Project #1: Remote Datacenter Temperature Management System - (RDTMS) v1.0 </b></h2>

<h3> <b>Background</b></h3>
Recent advancements in embedded computing technology have enabled a new generation of smaller and faster internet-of-things (IoT) devices. In research and development (and often in military contexts), the acronynm SWaP-C is used in reference to optimizing the Size, Weight, Power, and Cost of pysical devices, systems, and programs.  The convergence of allied technologies such as Edge computing, scalable Cloud services, AI/ML algorithm advancement, and ubiqutious high bandwidth network availability (e.g., 5G), have led an evolving distributed ecosystem that offers cost-effective, performant, scalable and resilent soutions to traditional hard technical challenges.  Although new technology offers benefits and avantages, there are also untended consequence that introduce new risks. The adoption of IoT technology into commercial and military domains has been stifled due to the significant risks associated with increased security vulnerabilities that result from lacking standardization and guidance and the architectural variance across the major pedigrees of device types.  Competing (and proprietary) vendor systems limits interoperability and signifiantly increases the scale and complexity of integrating IoT technology operational systems and environments.    

<h3> <b>Sample Problem Synopsis</b></h3>
Information technology (IT) infrastructure is one of the most important assets to data centric environment.  If IT equipment such as servers, firewalls, routers, switch panels and related systems were to overheat, it could significantly impact the performance, availability, and the reliability of critical information systems, potentually resulting in grave financial damage and even loss of life.  The application of new IoT technology and with the use of Cloud services can be used to achieve a lightweight, cost-effective solution that minimizes costs and overhead by automating certain datacenter maintenance operations such montoring and regulating temperature conditions.

<h3> <b>Project Description</b></h3>

The RDTMS (v1.0) is intended to be prototyped using the Raspberry PI (RPi) SBC (single board computer), version 2 or greater. The purpose is to developed a "smart" HVAC system to monitor temperature and humidity conditions, and automatically activate/deactivate an external HVAC unit when sensed operating conditions exceed specified thresholds. A LCD character display is used indicate HVAC operation (ON/OFF) status.  The system will automatically dispatch a recorded phone call or text message to alert maintenance operators when conditions exceed specified threshholds. If-This-Then-That (IFTTT) automation service is integated using a webhook exposed from an Azure function to facilite making phone call, sending the text message, or sending an email.  A downloadable Cloud-hosted (PaaS) web application will deployed to the Azure Cloud, and used to provide maintenance operators with a real-time visualization and telemetry monitoring capability that can be viewed using a desktop PC or mobile device.  

<div style="margin:1em;margin-left:0;padding:.5em;width:40%;height:15%;border:solid thin">
  <img src="images/d3.jpg" />
  <center> <p> Figure 1: RTDMS version 1.0 </p> </center>
</div>

<h3> <b>Objectives and Goals</b></h3>
The primary project objective is to enable cyber security analysts and systems engineers to develop the architectural awareness to reason critically about the design, security, and resiliency of IoT systems.  IoT systems consist of hetergenous parts, and is therefore important that analysts have a holistic understanding of the underlying architecure. This repository describes an active learning project that leads the student through the design and implementation of a (“Smart”) IoT prototype that provides remote datacenter condition monitoring, automated temperature regulation, and automated operator alerting. At each stage of the architecture design and implementation, a critical security analysis/assessment should be performed to identify and document identified vulnerabilities. A mitigation strategy should be developed and implemented for each identified case.  

<div style="margin:1em;margin-left:0;padding:.5em;width:55%;height:35%;border:solid thin" >
  <img src="images/vis.png" />
  <center> <p> Figure 2: Azure Cloud-Hosted (PaaS) TelemeMonitoring Web Application </p> </center>
</div>

<br>

<h3> <b> Concept Architecture Description </b> </h3>
The goal of this project is to design and implement a robust prototype solution for the sample problem above. Using the concept illustrated below, the implementation for the "Smart" HVAC prototype can be divided into four (4) basic tasks, consistent with the commonly accepted conceptual framework (4-layer) architecture shown below:

<div style="margin:6px;margin-left:0;padding:2px;width:75%;height:50%;border: solid thin" >
<img src="images/concept2.jpg" />
<center> <p> Figure 3: RTDMS Concept </p> </center>
</div>

<ol>
 <li> Construct the (Device) Hardware.</li>
 <li> Develop the code (called the driver) that runs locally on the RPi to manage the electronic components that implement the functionality of the device.</li>
 <li> Develop a serverless code function and deploy to the Azure Cloud as a FaaS (function-as-a-service) to monitor and process temperature and humidity conditions remotely, and initiate automated actions.</li>
 <li> Provide real-time visualizations using an Azure Cloud-host (PaaS) web application, and a custom Power Bi dashboard.</li>
 <li> Think critically about the security and resiliency inherent in the design of the underlying architecture, and identify and document identified vulnerabilities and recommend and implement a mitigation strategy.
</ol>

<br>

The commonly held conceptual architecture framework for testing and assessing IoT devices for security and resiliency is illustrated below:
<div style="margin:1em;margin-left:0;padding:.5em;width:55%;height:30%;" >
<img src="images/framework.jpg" />
<center> <p> Figure 4: Conceptual architecture framework for testing and assessing IoT devices </p> </center>
</div>

The functionality of IoT devices generally maps into these 4 layers, indicating the type of testing that should be performed. Compare this framework in Figure 3 (above) to the RTDMS concept architecture depicted in Figure 4 (above). From Figure 3, try to determine how the
system functionality maps into the testing framework in Figure 4.   

<br>

<h2> <b> Task 1: Construct the Device: </b> </h2>
<b>Device (Hardware) requirements: </b> RPi dev board (versions 2,3, and 4 suffice), and full-size breadboard consisting of the following electronic components:
<ul>
   <li>
     <b>Bosch BME20 sensor <a href="https://www.adafruit.com/product/2652">(example)</a></b>
     <ul>
       <li>low-cost precision sensor from Bosch for measuring humidity with ±3% accuracy, barometric pressure with ±1 hPa  absolute accuracy, and temperature with ±1.0°C accuracy
       </li>    
     </ul>
   </li>
   <li> 
      <b>5v Relay Board Relay Module 1 Channel <a href="https://www.amazon.com/dp/B09G6H7JDT?_encoding=UTF8&psc=1&ref_=cm_sw_r_cp_ud_dp_084P3W00V2BFR3BTGDKC">(example)</a></b>
      <ul>
        <li>is an electromagnetic switch used to programmatically activate/deactivate external devices (i.e., an HVAC unit).It works by using small currents to control separate (often larger) currents. When a small current is passed through the low-voltage (5v DC) input on the relay it activates the switch (using a coil) and completes the separate high voltage (120v AC) circuit (i.e., larger current).
        </li>
      </ul> 
  </li>  
   <li>
     <b>20x4 Character display <a href="https://www.amazon.com/dp/B082Y37WXG?psc=1&ref=ppx_yo2ov_dt_b_product_details">(example)</a></b>
      <ul>
        <li>The character display is used for displaying information about the IoT device, including its status and operating state (i.e., is HVAC unit or off, and the current temperature status in the environment).
        </li>
      </ul> 
  </li>
   <li>
     <b>5mm LED <a href="https://www.adafruit.com/product/299">(example)</a></b>
      <ul>
        <li> 
            The LED is used to indicate the device is transmitting temperature and humidity data by blinking the LED.
        </li>
      </ul> 
  </li>
</ul>
The electronic components connect to the RPi through the 40-pin general Purpose Input/Output (GPIO) header. The GPIO supports low-level pin access and serial bus protocols for communicating (input and output) between the RPi device and external electronic components.  

<div style="margin:1em;margin-left:0;padding:.5em;width:30%;height:15%;border:solid thin" >
<img src="images/cobbler.jpg" />
<center> <p> Figure 3: GPIO expansion (TCobbler) </p> </center>
</div>

The breadboard shown in Figure 3 (above) is paired with a GPIO expansion board to simplify prototyping with GPIO header.  This particular GPIO expansion board is often called a GPIO breakout, or simplify a T-Cobbler Plus connection. 

<div style="margin:1em;margin-left:0;padding:.5em;width:60%;height:30%;border:solid thin" >
<img src="images/rpigpio.png" />
<center> <p> Figure 4: GPIO Header Close Up </p> </center>
</div>

 RPi supports multiple pin numbering schemes (GPIO, BOARD) that determined how pins are identified and addressed by in source code.  This RTDMS project will use the GPIO scheme.  View the following reference for more detail on RPi supported pin number schemes: https://learn.sparkfun.com/tutorials/raspberry-gpio/gpio-pinout  Figure 4 (above) provides a close up view of the the GPIO header.  RPi supports serial bus protocols including I<sup>2</sup>C and SPI through the GPIO header.

<div style="background:lightblue;margin-left:1em;padding:1em">
<b>Note:</b> Inter-Integrated Circuit (I<sup>2</sup>C) is a well-known serial bus protocol for connecting integrated circuits (such as the BME280 temperature sensor) over low speed, short-distance serial communication. I<sup>2</sup>C is straight forward to use since it requires only two GPIO pins to operate: SDA (for data transfer), and SCL (for carrying the clock signal).  I<sup>2</sup>C and the similar serial peripheral interface (SPI) protocol are commonly used in embedded device applications such as gateways and home routing devices, as well as industrial/commercial devices for integrated circuit communication. See the following URL for additional detail on these protocols : <em> <u> https://learn.sparkfun.com/tutorials/i2c/all </u> </em>
</div>

<br>

<h3> <b> Assemble the Device Hardware </b> </h3>
With the RPi and unplugged from the power source, follow the design sketch shown below to install the electronic compnents. Install the BME280 sensor and the LCD character display onto the breadboard, and connect to the I2C bus pins SDA and SCK and described below:     

<div style="margin:1em;margin-left:0;padding:.5em;width:80%;height:50%;border:solid thin">
    <img src="images/rdtms.png" />
    <center> <p> Figure 5: RTDMS Device Sketch </p> </center>
</div>

<br>

<b>Complete the steps (1-14) below to construct the device: </b> The finished prototype should closely resemble Figure 5 (above). Note:the following tutorial (URL below) by Cam Soper is an excellent primer for understanding the basic breadboard prototyping concepts and code, with illustrations for connecting the BME280 sensor to the GPIO header: https://learn.microsoft.com/en-us/training/modules/create-iot-device-dotnet/2-construct-iot-hardware

<div style="background:lightblue;margin-left:1em;width:fit-content;padding:1em">
<b>Note:</b> care must be taken with connecting devices to the GPIO header. Improper electrical connections can permanently damage the Raspberry Pi 
</div>

1.	Connect one end of a <b><span style="color:red">“Red”</span></b> jumper wire to the 3.3v pin of the T-Cobber and the positive (+) terminal strip (same side 3.3v pin)
2.	Connect one end of a <b><span style="color:red">“Red”</span></b> jumper wire to positive (+) terminal strip and the VIN input pin on the BME280 sensor.
3.	Connect a <b><span style="color:#0066CC">“Blue”</span></b> wire to the SDA pin of the T-Cobbler, and the SDI pin on the BME280 sensor.
4.	Connect a <b><span style="color:orange">“Orange”</span></b> wire to SCL pin of the T-Cobbler, and the SCK pin on the BME280 sensor.
5.	Connect a <b><span style="color:black">“Black”</span></b> to a “GND” pin on 3.3v side of the T-cobbler, and connect it to negative terminal strip on the breadboard.
6.	Connect a <b><span style="color:black">“Black”</span></b> wire from “GND” pin on the BME280 sensor to the “negative (-) terminal strip on the breadboard.  
7.	Connect a <b><span style="color:green">“Green”</span></b> wire to GPIO pin 17 of the T-Cobbler, and to the anode (longer) positive (+) pin on the LED.
8.	Connect a 220-ohm resistor between LED cathode (shorter negative) pin and the negative (-) terminal strip on the breadboard.
9.	Connect a <b><span style="color:#8B8000">“Yellow”</span></b> wire to GPIO pin 21 of T-Cobber, and the signal (IN) pin on the relay.
10. Connect a <b><span style="color:red">“Red”</span></b> wire to the (5v) terminal strip pin of the relay, to the negative (-) to terminal strip on the breadboard.     
10.	Connect a <b><span style="color:black">“Black”</span></b> wire to the GND pin of the relay, to the negative (-) to terminal strip on the breadboard.     
11.	Connect a <b><span style="color:#0066CC">“Blue”</span></b> wire to the SDA pin of the T-Cobbler, and the SDA pin on the LCD character display
12.	Connect a <b><span style="color:orange">“Orange”</span></b> wire to SCL pin of the T-Cobbler, and the SCK pin on the LCD character display
13.	Connect a <b><span style="color:black">“Black”</span></b> wire from “GND” pin on the LCD character display to the “negative (-) terminal strip on the breadboard.  
14.	Connect a <b><span style="color:red">“Red” </span></b> wire from “VCC” pin on the LCD character display sensor to the “positive (+) (5v) terminal strip on the breadboard.  

<h3> <b> Initial Device Test: I<sup>2</sup>C bus communication: </b></h3>

Use the "i2cdetect" command as discussed in the following URL, to scan the I<sup>2</sup>C bus. The BME280 and LCD character display addresses should be displayed as 0x77 for the BME280, and 0x27 for the LCD character display.
If no addresses appear in the scan (or only one address) then either the circuit configuration is incorrect, and/or potentially the BME280 sensor working properly.
https://learn.adafruit.com/scanning-i2c-addresses/raspberry-pi


<div style="background:#FF2A00;color:white;margin-left:1em;width: fit-content; padding:1em">
<img src="images/shock.jpg" style="width:50px; height:50px; float:left; margin:.5em">
Note: The RTDMS sketch (above) is shown with an LED acting as a stand-in for the HVAC system.  This is primarily for simplifying testing the application logic.  The completed prototype uses the relay to control a separate, high-voltage circuit required to power external devices (the HVAC unit). It is important to ensure that the relay is properly connected to the high-voltage side!  Incorrect connection of the relay to a 120v AC outlet can result in a dangerous electrical shock and/or a fire.  The mentor will assist in ensuring the relay is properly connected for activating the HVAC unit.  The figure below illustrates the completed RTDMS prototype with the connection for the 120V AC power outlet. 
</div>

<div style="margin:1em;margin-left:0;padding:.5em;width:60%;height:30%;border:solid thin" >
<img src="images/ac_connextion.jpg" />
<center> <p> Figure 6: RTDMS prototype with 120v AC Outlet Connection </p> </center>
</div>


<h2><b> Step 2: Developing RTDMS Driver Software </b></h2>
<h3> <b> Getting Started: </b></h3>
The RTDMS driver is the code that runs on the physical device.  This includes the code for reading the BME280 (TPH) sensor data using I2C serial bus protocol, and packaging that data as telemetry to dispatch to the Cloud.   As you will see below, the majority of the code has been provided. Your job is understand and complete each of the code as described in subsequent sections. 
The project was prepared using Ubuntu 22.04 development host, using C# programming and .Net 6.0 SDK environment with standard .net IoT NuGet packages, and the Visual Studio (VSCode) editor. The Raspberry 3 target board is single board computer (SBC) with an ARM-64bit CPU, running the latest version of Raspberry Pi OS (Debian Linux distro).

 <h3><b>Raspberry Pi Setup</b></h3>
Refer to the following URL, follow the documentation to download and install the Raspberry Pi Imager to a computer with an SD Card reader.  Insert the SD card into the computer: https://www.raspberrypi.com/software/operating-systems/
The Imager will provide an option to choose "Rasperry Pi OS (other)". Select  Raspberry Pi OS (64-bit Debian Bullseye) Pi Desktop as shown in below. The sproket (cog) wheel on the lower right of the imager window allows you to configure the Rasberry Pi prior to writing the image to the SD card. Configure settings including username, network ssid, VNC, and SHH etc. as shown below   

<div style="margin:1em;margin-left:0;padding:.5em;width:50%;height:25%;border:solid thin" >
    <img src="images/pi.jpg" />
     <img  src="images/pi4.jpg" />
    <center> <p> Figure 7: Raspberry PI Imager:  Use cog on the right to specify required configuration settings </u> </p> </center>
</div>

<div style="margin:1em;margin-left:0;padding:.5em;width:50%;height:25%;border:solid thin" >
    <img src="images/pi2.jpg" />
    <center> <p>  Figure 8: Select Raspberry Pi OS (other) </p> </center>
</div>

<div style="margin:1em;margin-left:0;padding:.5em;width:50%;height:25%;border:solid thin" >
    <img src="images/pi3.jpg" />
    <center> <p>  Figure 9: Use the 64-bit version </p> </center>
</div>

<h3><b>Complete the Raspberry Pi OS Configuration</b></h3>
Upon completing Raspberry Pi OS isntallation, open a terminal, and run the <i>raspi-config</i> command. 
Ensure the following services are enabled:
1.	SSH (Secure Shell)
2.	VNC 
3.	I<sup>2</sup>C (Inter-Integrated Circuit) 

<div style="background:lightblue;margin-left:1em;padding:.5em;width:fit-content;">
    <b>Note:</b> Refer to the following URL to for details using raspi-config to enable I<sup>2</sup>C: <br>
     <u> https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c </u>
</div>

<br>


<h3><b> Create an Microsoft Azure Cloud Account: Student Subscription </b></h3>
Referring to the following URL, use your university or school email to sign up a $100 Azure credit (good for 12 months): https://azure.microsoft.com/en-us/free/students/

Refer to the following URL to create an Azure IoT Hub Service (using the free tier), and register a new IoT device.  Name the device the "RTDMS_dev1". Copy the device the primary connection string, you will need to configure the appsettings.json configuration file in thge next section.  The connection string is needed for authenticating the RTDMS device, and the Azure Cloud (IoT Hub service).
https://learn.microsoft.com/en-us/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started#create-an-iot-hub


<h3> <b> Ubuntu 22.04 (Development Host) Setup </b></h3>
<h4> Download Visual Studio Code (VSCode) editor (for Ubuntu)<h4>
```sh
sudo apt update
sudo apt install code
```
<h4> Open VSCode, and install the official (Microsoft) C# language extension as illustrated (below) </h4>
<div style="margin:1em;margin-left:0;padding:.5em;width: fit-content;height:40%;border:solid thin" >
    <img src="images/extension1.jpg" />
    <center> <p> <u> Official C# VSCode extension </u> </p> </center>
</div>

<h4> Install .Net 6.0 (LTS) for Linux (x64) on the Development Host): </h4>
<div style="margin:1em;margin-left:0;padding:.5em;width:70%;height:40%;border:solid thin" >
    <img src="images/dotnet.jpg" />
    <center> <p> VSCode <u> https://code.visualstudio.com/download </u> </p> </center>
</div>

Extract the downloaded file to $HOME/dotnet folder and set using export to execute the dotnet command from current session
```sh
# note: substitute vers. 6.0.411 for other downloaded .Net SDK versions 
mkdir -p $HOME/dotnet && tar zxf dotnet-sdk-6.0.411-linux-x64.tar.gz -C $HOME/dotnet
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet

# Run nano editor to edit the .bashrc
nano ~/.bashrc
 
# Copy the commands below to the .bashrc
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
 
# Run this command so the terminal session will use the new settings
source ~/.bashrc
```

Verify the SDK is installed, by listing the SDKs installed on the host
```sh
dotnet --list_sdks
```
<div style="margin:1em;margin-left:0;padding:.5em;width:70%;height:50%;">
    <img src="images/sdk_list.jpg" style="border:solid thin" />
    <center> <p> List dotnet SDKs installed </p> </center>
</div>

<h2> <b> Create the .Net (RTDMS-V1) Solution (sln) </b></h2>
Open terminal, and use the dotnet CLI (command line interface) to run the command below.  

```sh
# Open command termninal, navigate to the home (~) folder and make a projects folder
cd ~
mkdir projects && cd projects

# 1. Create the solution (sln), and make that the current folder:                      
     dotnet new sln -o RTDMS-V1 
     cd RTDMS-V1

# 2. Create the RTDMS-driver project: 
     dotnet new console -o RTDMS-driver --use-program-main

# 3. Create a class library called: TelemModel:
    dotnet new classlib –o TelemModel

# 4. Add the RTDMS-driver project to the solution (sln): 
     dotnet sln add RTDMS-driver/RTDMS-driver.csproj 

# 5. Add the Telemetry project to the solution (sln): 
     dotnet sln add TelemModel/TelemModel.csproj 

# 6. Navigate to the RTDMS project folder: 
    cd RTDMS-driver 
        # Add the TelemModel project reference:
        dotnet add RTDMS-driver.csproj reference ../TelemModel/TelemModel.csproj
       
        # Add the following NuGet packages to the  RTDMS-driver project:
        # IoT Gpio) package:            
        dotnet add package System.Device.Gpio 
        
        # IoT (Bindings) package:       
        dotnet add package IoT.Device.Bindings 
        
        # JSON config provider package: 
        dotnet add package Microsoft.Extensions.Configuration.Json
        
        # config binder package:       
        dotnet add package Microsoft.Extensions.Configuration.Binder
        
        # Azure IoT Hub device SDK package to connect devices to Azure IoT Hub: 
        dotnet add package Microsoft.Azure.Devices.Client
```

<h3> C# .Net IoT (NuGet) Library packages: </h3>
<h4> Communication with the device components using the I2C through the GPIO header is provided by the .Net IoT library packages: </h4>

<b> System.Device.Gpio - </b> supports general-purpose I/O (GPIO) pins, PWM, I2C, SPI and related interfaces for interacting with low level   hardware pins to control hardware sensors, displays and input devices on single-board-computers; Raspberry Pi, BeagleBoard, HummingBoard, ODROID, and other single-board-computers that are supported by Linux
            
<b> IoT.Device.Bindings </b> - contains device bindings to streamline app development by wrapping System.Device.Gpio. It contains classes representing a wide array of common IoT sensors and other devices. It's a community-driven, open-source project, and anybody can add new device support.
            
<b> Supported Operating Systems - </b>  The .NET IoT Libraries will run on any operating system that supports the .NET framework. This includes most Linux distributions (and Raspberry Pi OS is a Debian distro) that support AMD/AMD64 and ARM/ARM64. Note: .Net will not run on RPi version 1 using the older ARM v6 CPU)

<h3> <b> Prepare the RTDMS code </b></h3>

```sh
# Nativate to the RTDMS_V1 solution (sln) folder
cd ~/projects/RTDMS-V1

# open VScode from the sln folder
code .
```
As shown below, Create a folder name <b>src</b> under the <b>RTDMS-driver</b> project folder 
<div style="margin:1em;margin-left:0;padding:.5em;width:70%;height:50%;border:solid thin">
    <img src="images/sln_view.jpg"  />
    <center> <p> VSCode: RDTMS Solution folder </p> </center>
</div>

Under the "RDTMS_driver/src" folder, create the following C# code (.cs) files, and copy code content as shown below for each file.
1. Move the existing Program.cs file in "RDTMS_driver/" to the "RDTMS_driver/src" folder, and replace the contents of the file with the code shown below:

```csharp
// Description: Interim (version 1) IoT bootcamp development project (Remote Data Center Monitoring) prototype
// Skill Level:  university engineering or comp sci ( sophomore and higher)

// This file is main .exe (client) RDTMS driver entry point
using Microsoft.Extensions.Configuration;

namespace viceroy
{
    public class RTDMS_Driver_Exec 
    { 
        static void Main(string[] args)
        {    
            // Build a config object, using JSON providers.
            // https://learn.microsoft.com/en-us/dotnet/core/extensions/configuration
            IConfiguration config = new ConfigurationBuilder()
                .AddJsonFile("appsettings.json")
                .Build();

            Console.WriteLine("\t** RTDMS IoT driver version 1.0 ** ");
            // instantiate the RTDMS driver object
            // Note: the using ensires the that "dispose is called when the object
            // goes out of scope.  Dispose ensures that plaform resources are freed, not waiting
            // for the garbabge collector
            using RTDMS_Driver driver = new RTDMS_Driver();

            Console.WriteLine("\t\tHVAC using pin {0}", driver.Settings.HVACPin);
            Console.WriteLine("\t\tLED  using pin {0}", driver.Settings.LEDPin);

            // start the RDTMS driver (starts the main driverTask)
            driver.Start();

            // stop the RTDMS driver (this blocks until the driverTask completes when the user exits the menu ) 
            driver.Stop();
        }     
    }
}

```

2. Create a new .cs file called: RTDMS.cs in "RDTMS_driver/src". Copy and Paste the code below and save the file.
 RTDMS.cs implements the primary RTDMS-driver functionality.
```cs
// Description: Interim (version 1) IoT bootcamp development project (Remote Data Center Monitoring) prototype
// Skill Level:  university engineering or comp sci ( sophomore and higher)

// This file implements the primary RDTMS driver code functionality
// sources:  derived from original example by Cam Soper: https://www.linkedin.com/in/camthegeek

// MQTT / Security refs 
// IOT Hub Security: https://docs.microsoft.com/en-us/azure/iot-hub/iot-concepts-and-iot-hub#device-identity-and-authentication
// MQTT:  https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-mqtt-support

using System;
using System.Device.Gpio;
using System.Device.I2c;
using System.Text;
using System.Text.Json;
using Iot.Device.Bmxx80;
using Iot.Device.Bmxx80.ReadResult;
using Microsoft.Azure.Devices.Client;
using Microsoft.Extensions.Configuration;

#nullable disable

namespace viceroy
{
    public class RTDMS_Driver : IDisposable
    {
        public bool HVAC_On = false;
        private I2cConnectionSettings i2cSettings;
        private I2cDevice i2cDevice;
        private GpioController gpio;
        private Bme280 bme280;
        private LCDWriter lcd_writer;
        private IotHubClient hub_client;
        private Task driverTask;
        private Task transmitTask;
        private object transmitLockObj;
        private CancellationTokenSource ctsTransmitTelem;
        
        // properties
        public RDTMS_Settings Settings { get; set; }
        public int HVAC_Pin { get; set; }
        public int LED_Pin { get; set; }
        public int TransmitInterval;

        int transmitCount = 0;

        // constructor 
        public RTDMS_Driver()
        {
            try
            {
                // Build/read a configuration object, using JSON providers.
                // https://learn.microsoft.com/en-us/dotnet/core/extensions/configuration
                IConfiguration config = new ConfigurationBuilder()
                   .AddJsonFile("appsettings.json")
                   .Build();

                // Get values from the appsettings.json configuration given their key and target value type.
                Settings = config.GetRequiredSection("Settings").Get<RDTMS_Settings>();

                // set the HVAC and LED GPIO pins 
                HVAC_Pin = Settings.HVACPin;
                LED_Pin = Settings.LEDPin;

                // Get a reference to a device on the I2C bus
                i2cSettings = new I2cConnectionSettings(1, Bme280.DefaultI2cAddress);

                // initialize the device (instance) using, the BME280 default bus address
                i2cDevice = I2cDevice.Create(i2cSettings);

                // Finally, create an instance of BME280, using device settings configured above)
                bme280 = new Bme280(i2cDevice);

                // Initialize the GPIO controller for communication with Rasspberry Pi, using logical pin numbering scheme
                gpio = new GpioController(PinNumberingScheme.Logical);

                // Open the HVAC pin for output, set to off (low voltage)
                gpio.OpenPin(Settings.HVACPin, PinMode.Output);
                gpio.Write(Settings.HVACPin, PinValue.Low);

                // Open the transmit LED indicator pin for output, set to off (low voltage)
                gpio.OpenPin(Settings.LEDPin, PinMode.Output);
                gpio.Write(Settings.LEDPin, PinValue.Low);

                //construct an instance of the LCD_writer (MaxLines, and LineLen are set in appsettings.json)
                //note: i2c bus address is 0x27
                lcd_writer = new LCDWriter(1, 0x27, Settings.LCDMaxLines, Settings.LCDLineLen);
                lcd_writer.On(true); // turn the LCD display on

                // construct an instance of the IoTHub to enable dbidirectional MQTT communication the Azure Iot hub service
                // Note: this depends on Microsoft.Azure.Devices.Client package
                hub_client = new IotHubClient(Settings, TransportType.Mqtt, this);

                // cancelation token for stopping the transmit task
                ctsTransmitTelem = new CancellationTokenSource();

                // critical section (lock), used for setting the interval rate
                transmitLockObj = new Object();

                // set the default transmit interval (ms -- millseconds)
                TransmitInterval = 1000;

                // trap ctrl-c press
                Console.CancelKeyPress += (s, e) =>
                {
                    Console.WriteLine("Choose menu option \"X\" to exit the program");
                    e.Cancel = true;
                };
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"{ex}");
            }
        }

        /* complete this function */
        public (double, double, double) ReadBME280()
        {
            // *** 1. write the code to Read the BME280 sensor, and return 3-tuple (temp, hum, pressure)   
            double temperatureF, humidityPercent, decapascals;
            temperatureF = humidityPercent = decapascals = 0.0;
            return (temperatureF, humidityPercent, decapascals);
        }

        // this a cleanup function, runs when shutting thge device down
        public void HandleCloseCommmand()
        {
            if (HVAC_On)
            {
                Console.WriteLine("Shuting down HVAC unit ");
                gpio.Write(HVAC_Pin, PinValue.Low);
            }

            // if the transmit LED is high, shut it down
            if (gpio.Read(LED_Pin) == PinValue.High)
            {
                gpio.Write(LED_Pin, PinValue.Low);
            }

            // Close the pin before exit
            gpio.ClosePin(HVAC_Pin);
            gpio.ClosePin(LED_Pin);

            // turn off lcd display
            lcd_writer.On(false);
        }

       /*  complete this function */
        void UpdateSendInterval()
        {
            // this is a basic lock called a monitor (synchonization primative --critical section) used to guard concurrent access to data
            // sharted between threads. In this case, the data transmission rate variable: "TransmitInterval" 

            // Note see resource: https://www.c-sharpcorner.com/UploadFile/de41d6/monitor-and-lock-in-C-Sharp/
            //                    https://dotnettutorials.net/lesson/multithreading-using-monitor/
            
            // thread acquires the lock, enters the  critcal section  
            lock (transmitLockObj)
            {
                // *** thread is with critical section  ***
                // write the code to perfrom the following steps...
                
                /* 1. prompt user for new interval rate (in milliseconds (ms) e.g. 1 sec == 1000 ms)
                   2. Read the new the rate from the user via command line (STDIN)
                   3.  verify what the user input is valid 
                   4.  set the TransitInterval variable with value read from the user
                   5. write a message on the console (STDOUT), indicating the messaage rate has been updated
                */ 

                // *** note: thread exiting the critical section
            }
        }

         /*  complete this function */
        void SendAzureCompatibleTempHumMessage(string device_id, double temp, double hum)
        {    
            // 1.  capture the telemetry in an instance of the telemetry model variable
            Telem telemetryDataPoint = new Telem
            {
                deviceId = device_id,
                temperature = temp,
                humidity = hum,
                messageId = transmitCount++
            };

            // *** 2.  write the code to Create JSON message: serialize the telemetry data
            // var telemetryDataString = 
                   
            // *** 3. write the code to Encode the serialized object using UTF-8 so it can be parsed by IoT Hub when
            //         processing messaging rules.

            // *** 4. write code to Send the message to the IoT hub.
           
            // Console.WriteLine(string.Format("[{0}] {1}", transmitCount, telemetryDataString));

            /* Note: use this online resource to complete 1-4 of thgs function:
            https://github.com/Azure/azure-iot-sdk-csharp/blob/main/iothub/device/samples/getting%20started/SimulatedDevice/Program.cs

            
            /*  Exameple Building raw messages (don't use this):
             string message_template = string.Format("{\"messageId\":{0},\"deviceId\":\"{1}\",\"temperature\":{2},\"humidity\":{3}}", ++msgCount, device_id,  temp, hum );
            Microsoft.Azure.Devices.Client.Message m = new Microsoft.Azure.Devices.Client.Message(Encoding.ASCII.GetBytes(message_template));
            iotClient.SendDeviceToCloudMessagesAsync(m).Wait();
            Debug.WriteLine(message_template);
            */
        }

        public void TransmitTelemety()
        {
            // a task is like a thread, but a higher level abstraction
            transmitTask = Task.Run(() =>
            {
                while (!ctsTransmitTelem.IsCancellationRequested)
                {
                    var telem = ReadBME280();

                    //flash the transmit LED, turn on
                    gpio.Write(LED_Pin, PinValue.High);

                    // send telemetry to Azure IoT Hub
                    SendAzureCompatibleTempHumMessage(Settings.DeviceId, telem.Item1, telem.Item2);

                    // thread acquires the lock, enters the  critcal section
                    // Note see resource: https://www.c-sharpcorner.com/UploadFile/de41d6/monitor-and-lock-in-C-Sharp/
                    //                    https://dotnettutorials.net/lesson/multithreading-using-monitor/
                    lock (transmitLockObj)
                    {
                        // flash the transmit LED, turn on
                        gpio.Write(LED_Pin, PinValue.Low);
                        
                        // sleep for the for duration od TransmitInterval
                        Thread.Sleep(TransmitInterval);
                    }

                    gpio.Write(LED_Pin, PinValue.Low);
                }

                // dispose of cancelation token, and instiate a new for next time the function runs
                ctsTransmitTelem.Dispose();
                ctsTransmitTelem = new CancellationTokenSource();
            });
        }

        bool IsTransmiting()
        {
            if(transmitTask != null)
               return !transmitTask.IsCompleted;
            return false;
        }

        // *** Complete this function *** /
        public void External_HVAC(bool onoff, string LCD_message)
        {
            HVAC_On = onoff;
            if(HVAC_On)
            {
                 //  *** 1. write the the code to turn On the HVAC
                Console.WriteLine("HVAC On not implementated");
            }
            else
            {
                //  *** 2. write the the code to turn On the HVAC
                 gpio.Write(HVAC_Pin, PinValue.Low);
            }

            Console.WriteLine($"{LCD_message}");
            //  *** 3. write the code to display the message on the LCD character display 
        }

        bool ExecuteCommand(string commandText)
        {
            switch (commandText.ToLower())
            {
                case "x":
                    Console.WriteLine("Exiting RTDMS...");
                    HandleCloseCommmand();
                    return true;

                case "h":
                    {
                        string HVAC_msg = "HVAC Off";
                        if (HVAC_On = !HVAC_On)
                        {
                           HVAC_msg = "HVAC On";
                        }
                       
                        External_HVAC(HVAC_On, HVAC_msg);    
                    }
                    break;
                case "t":
                    {
                        if (IsTransmiting())
                        {
                            ctsTransmitTelem.Cancel();
                            transmitTask.Wait();
                        }
                        else
                        {
                            TransmitTelemety();
                        }
                    }
                    break;
                case "i":
                    UpdateSendInterval();
                    break;
                case "s":
                    {
                        var output = ReadBME280();
                        Console.WriteLine("DEVICE STATUS");
                        Console.WriteLine("-------------");
                        Console.WriteLine($"HVAC: {(HVAC_On ? "ON" : "OFF")}");
                        Console.WriteLine($"Temperature: {output.Item1:0.#}dF");
                        Console.WriteLine($"Relative humidity: {output.Item2:#.##}%");
                        string lcd_msg = $"T:{output.Item1:0.#}dF " + $"H:{output.Item2:#.#}%";

                        lcd_writer.WriteMessage(lcd_msg);
                    }
                    break;
                default:
                    Console.WriteLine("Unknown command");
                    break;
            }
            return false;
        }

        void DisplayMenu()
        {
            string hvac_status = HVAC_On ? "Off" : "On";
            string transmit_status = (!IsTransmiting()) ? "Transmit" : "Stop Transmiting";
            Console.WriteLine("---------------");
            Console.WriteLine("RDTMS v1.0 Menu");
            Console.WriteLine("---------------");
            Console.WriteLine("\"S\": - display current temperature/humidity");
            Console.WriteLine($"\"H\": - turn HVAC {hvac_status}");
            Console.WriteLine($"\"T\": - {transmit_status} Telemetry To Azure IoT Hub service");
            Console.WriteLine("\"I\": - Change telemetry transmit interval (1000ms -default )");
            Console.WriteLine("\"X:\" - Close the  RDTMS driver");
            Console.Write("Command:-> ");
        }

        public void Start()
        {
            // create a Task to connect to asychronously to the IoT hub:
            // see background info here: https://dotnettutorials.net/lesson/asynchronous-programming-in-csharp/
            driverTask = Task.Run(() =>
            {
                // prior to displaying the menu for the first time connect, established TLS connection to Azure IoT Cloud 
                hub_client.Start();

                if (hub_client.Connected)
                {
                    Console.WriteLine("Using Shared Access Signature (SAS - connectionString) to authenticate with Azure IoT service, please wait...");
                    Console.WriteLine("Successfully Connected To Azure Cloud (IoT Hub) Service, using MQTT over TLS.");
                }
                else
                {
                    Console.WriteLine("Error connecting (or already connected) to the Azure Cloud");
                }

                bool exit = false;
                while (!exit)
                {
                    DisplayMenu();
                    string commandText = Console.ReadLine();
                    exit = ExecuteCommand(commandText);
                }

                Console.WriteLine("Closing Azure IoT Connection...");
                hub_client.Close();
                if (!hub_client.Connected)
                    Console.WriteLine("Disconnected from Azure Cloud");
                else
                    Console.WriteLine("Eror disconnecting from the Azure Cloud");
            });
        }

        public void Stop()
        {
            // wait on the driver task to make the main thread (task) block
            driverTask.Wait();
        }

        // diespose frees any native platform (non CLR managed) resources
        public void Dispose()
        {
            if (bme280 != null)
                bme280.Dispose();

            if (lcd_writer != null)
                lcd_writer.Dispose();

            if (i2cDevice != null)
                i2cDevice.Dispose();

            if (gpio != null)
                gpio.Dispose();

            if (hub_client != null)
                hub_client.Dispose();

            if (ctsTransmitTelem != null)
                ctsTransmitTelem.Dispose();

            Console.WriteLine("All Disposed");
        }
    }
}
```
3. Create a new .cs file called: LCDWriter.cs in "RDTMS_driver/src". Copy and Paste the code below and save the file.
   LCDWriter.cs provides a reusable C# package for the writing messages to LCD character displays.

```cs
// Description: Interim (version 1) IoT bootcamp development project (Remote Data Center Monitoring) prototype
// Skill Level:  university engineering or comp sci ( sophomore and higher)

// LCDWriter is a utility class for displaying messages on LCD character displays 

using Iot.Device.CharacterLcd;
using Iot.Device.Pcx857x;
using System;
using System.Device.Gpio;
using System.Device.I2c;

namespace viceroy
{
    public class LCDWriter : IDisposable
    {
        I2cDevice i2c;
        Pcf8574 driver;
        Lcd2004 lcd;

        int line_len_;
        int max_lines_; 

        public LCDWriter(int busId, int deviceAddress, int maxLines, int lineLen)
        {
            i2c = I2cDevice.Create(new I2cConnectionSettings(busId, deviceAddress));
            driver = new Pcf8574(i2c);
            lcd = new Lcd2004(registerSelectPin: 0,
                                    enablePin: 2,
                                    dataPins: new int[] { 4, 5, 6, 7 },
                                    backlightPin: 3,
                                    backlightBrightness: 0.1f,
                                    readWritePin: 1,
                                    controller: new GpioController(PinNumberingScheme.Logical, driver));
        
            line_len_ = lineLen;
            max_lines_ = maxLines;
        }


        public void WriteMessage(string message)
        {
            Clear();
            int numLines = (int)Math.Ceiling((double)message.Length / line_len_);

            int line_num = 0;
            int startPos = 0;
            for (line_num = 0; ((line_num < numLines - 1) && (line_num < max_lines_)); ++line_num)
            {
                WriteMessageLine(message.Substring(startPos,line_len_), line_num);
                startPos += line_len_;
            }

            WriteMessageLine(message.Substring(startPos, message.Length-startPos), line_num);
        }


        public void WriteMessageLine(string message, int lineNum, int startPos = 0)
        {
            lcd.SetCursorPosition(startPos, lineNum);
            lcd.Write(message);
        }

        public void Clear()
        {
            lcd.Clear();
        }

        public void On(bool on = false)
        {
            lcd.BacklightOn = on;
        }

        public void Dispose()
        {
            lcd.Dispose();
            driver.Dispose();
            i2c.Dispose();
        }

#if TEST_LCD_WRITER
        static void Main(string[] args)
        {
            Console.WriteLine("*** Test LCD Writer *** ");
            LCDWriter lcd_writer = new LCDWriter(1, 0x27);
            lcd_writer.On(true);

            int currentLine = 0;

            while (currentLine < 4)
            {

                lcd_writer.Clear();
                lcd_writer.WriteMessage(DateTime.Now.ToShortTimeString(), currentLine);

                currentLine++;
                Thread.Sleep(1000);
            }

            lcd_writer.On(false);
        }
#endif
    }
}
```

4. Create a new .cs file called: IoTHubClient.cs in "RDTMS_driver/src". Copy and Paste the code below and save the file.
   LCDWriter.cs provides a reusable C# package for the writing messages to LCD character displays.
   IoTHubClient is a utility class for connecting to the Azure IoT hub using Shared Access Signature (SAS). It facilites device-to-cloud (d2c), and cloud-to-device (c2d) messaging 
```cs
// Description: Interim (version 1) IoT bootcamp development project (Remote Data Center Monitoring) prototype
// Skill Level:  university engineering or comp sci ( sophomore and higher)

// IoTHubClient is a helper/utility class for connecting to the Azure IoT hub.

#nullable disable

using Microsoft.Azure.Devices.Client;
// using Newtonsoft.Json;
using System.Diagnostics;
using System.Text.Json;

namespace viceroy
{
    public class IotHubClient : IDisposable
    {
        private DeviceClient deviceClient;
        private readonly RDTMS_Settings settings_;
        private RTDMS_Driver _driver;

        public bool Connected {get; set;}

        public IotHubClient(RDTMS_Settings settings, TransportType tt, RTDMS_Driver driver)
        {
            settings_ = settings;
            Connected = false;
            deviceClient = DeviceClient.CreateFromConnectionString(settings_.ConnectionString, tt);
            _driver = driver;
        }

        public void Start()
        {          
            // Source: https://learn.microsoft.com/en-us/azure/iot-hub/iot-hub-dev-guide-sas?tabs=node
            //         https://learn.microsoft.com/en-us/azure/iot-hub/iot-hub-mqtt-support

            if (!Connected)
            {
                // open the connection to the Azure IoT Hub 
                deviceClient.OpenAsync().Wait();

                deviceClient.SetMethodHandlerAsync("ControlRelay", ControlRelay, null).Wait();

                //on and off (boolean) message type:
                //await deviceClient.SetMethodHandlerAsync("ControlLED", ControlLED, null);
                Connected = true;
            }
        }

        public void Close()
        {
            if (Connected)
            { 
                deviceClient.CloseAsync().Wait();
                Connected = false;
            }
        }

        private Task<MethodResponse> ControlRelay(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine(String.Format("method ControlRelay: {0}", methodRequest.DataAsJson));
            try
            {       
                // OnOffMethodData m = JsonConvert.DeserializeObject<OnOffMethodData>(methodRequest.DataAsJson);
                OnOffMethodData status = JsonSerializer.Deserialize<OnOffMethodData>(methodRequest.DataAsJson);
                _driver.External_HVAC(status.onoff, (status.onoff) ? "HVAC Remote On" : "HVAC_Remote Off");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"{ex.Message}");
                //   this.callMeLogger(String.Format("Wrong message: {0}", methodRequest.DataAsJson));
                return Task.FromResult(new MethodResponse(400));
            }
            //this.callMeLogger(methodRequest.DataAsJson);
            return Task.FromResult(new MethodResponse(200));
        }

        public async Task SendDeviceToCloudMessagesAsync(Message message)
        {
            await deviceClient.SendEventAsync(message);
        }

        public void Dispose()
        {
            deviceClient.Dispose();
        }
    }

     class OnOffMethodData
    {
        public bool onoff { get; set; }
    }
}
```

5. Create a new .cs file named: Settings.cs in "RDTMS_driver/src". Copy and Paste the code below and save the file.
   Settings.cs provide data model for reading JSON configuration values from appsettings.json, used to configure the RTDMS application
```cs 
// Description: Interim (version 1) IoT bootcamp development project (Remote Data Center Monitoring) prototype
// Skill Level:  university engineering or comp sci ( sophomore and higher)
// RDTMS_Settings, capture settings read from appsettings.json

#nullable disable

namespace viceroy
{
    public sealed class RDTMS_Settings
    {
        public string ConnectionString { get; set; }
        public int TransmitInterval { get; set; }
        public int HVACPin { get; set; }
        public int LEDPin { get; set; }
        public string DeviceId { get; set; }
        public int LCDMaxLines { get; set; }
        public int LCDLineLen { get; set; }
    }
}
```
6. Create an file named: appsettings.json in "RDTMS_driver/src". Copy and Paste the JSON content below, and save the file.
   Replace "ConnectionStringValue" with the primary connecting string for the "RTDMS_dev1" registered with IoT Hub created previously.
   appsettings.json captures the application setting used to configure the RTDMS application.  This appsettings.json is read during 
   application startup to populate initial the configuration settings for the RTDMS driver.

```json
{
  "Settings": 
  {
    "ConnectionString": "ConnectionStringValue",
    "DeviceId": "DeviceId",
    "HVACPin": 21,
    "LEDPin": 17,
    "TransmitInterval": 1000,
    "LCDMaxLines": 2,
    "LCDLineLen": 16
  }
}
```

7. In project folder "TelemModel/",  rename Class1.cs to Telem.cs replace the file content with the code below, and save the file.
```cs
// Description: Interim (version 1) IoT bootcamp development project (Remote Data Center Monitoring) prototype
// Skill Level:  university engineering or comp sci ( sophomore and higher)

// device telemetry model class

#nullable disable

namespace viceroy
{
    public class Telem
    {
        public int messageId { get; set; }
        public string deviceId { get; set; }
        public double temperature { get; set; }
        public double humidity { get; set; }
    }
}
```

<h3> <b> Building and Deploying the RTDMS driver to the Raspberry PI </b></h3>
At this point, the RTDMS driver should compile successfully, with no errors and no warnings.
To Test, open a terminal in the VScode editor, navigate to the solution folder: <u>cd RTDMS-V1/</u>, and issue the command:
<u> "dotnet build" </u> to compile all of the projects in the solution as shown in the example screen shot below.
<div style="margin:1em;margin-left:0;padding:.5em;width:70%;height:50%;border:solid thin">
    <img src="images/build.jpg"  />
    <center> <p> VSCode: RDTMS Solution folder </p> </center>
</div>

If the build command displays errors or warnings, then revist the steps for under "Preparing the code" above
Athough the code compiles succesfully, it will not run on the develop host because the builds targets hardware 
of the Raspberry Pi. Therefore, we need build and upload the code to the Raspberry Pi 
<br><br>

 <h3><b> Deploy the RTDMS driver code to the Raspberry Pi </b></h3>
To develop and and test the RTDMS code, it must be deployed to target hardware device. For this project, the target hardware is the prototype RTDMS device developed on the full size breadboard, and connected to a Raspberry Pi via the GPIO header. The RTDMS code logic is uploaded and executed on the Raspberry Pi as Linux process. This code is developed using standard dotnet IoT libraries (NuGet) packages to drive the hardware prototype through the GPIO header.      
RTDMS code deployment to Raspberry Pi can be accomplished using two commands, saved to a script to run each time the cocode is uploaded to the Raspberry PI.
Commands:
1. The <em> dotnet publish --runtime linux-arm64 --self-contained </em>  command builds the RTDMS application application code for self-contained deployment to Raspberry PI target CPU architecture.

This command creates a directory with RTDMS binaries and all of the depenencies required for a "self contained" deployment targeting linux-arm64 runtime. 

<div style="background:lightblue;margin-left:1em;padding:1em;margin-bottom:.5em">
   Note the location of the publish folder: <u> RDTMS_driver/bin/Debug/net6.0/linux-arm64/publish </u>
</div>

The option <em> --runtime linux-arm64 </em> generates binaries compiled for the ARM (64-bit) CPU architecure. The <em> --self-contained </em> option packages
the .Net CLR (virtual machine) runtime along along side the RTDMS application deployment binaries. Packaging the runtime with RTDMS binaries carries the advantage of not 
requiring the .Net SDK to be installed on the Raspberry Pi OS system.  

<div style="background:lightblue;margin-left:1em;padding:1em;margin-top:.5em">
  <b> Note: </b> Although self contained deployments result in a larger set of files, and bigger deployment footprint to copy to target device, it also greatly simplifies deployment
  portability, since the runtime and all of the dependencies required to run the application are packaged together.  Self contained deployments are the basis for packaging
  and deployment using docker (container) images.     
</div>

2. The scp (secure copy) command is used to copy the files from the publish folder to the deployment location on the Raspberry Pi.  
For example, the commmand:  <em> scp RTDMS_driver/bin/Debug/net6.0/linux-arm/publish/* pi@192.168.43.160:~/RTDMS_deployment" </em> secure copies all of the
files in publish folder to the remote raspberry Pi folder: "~/RTDMS_deployment".  "pi" is the specified username, and "192.168.43.160" is the example IP address of the Raspberry Pi. 

Create a file named: <em> deploy-script.sh </em> in "RDTMS_driver/src". Copy and Paste the content shown below, and save the file.

```sh
# 1. Compile for the ARM (64-bit) architecture, and publish the RTDMS-driver to folder: bin/Debug/net6.0/linux-arm64/publish for deployment to RPi target device
dotnet publish  --sc -r linux-arm64  

# 2. secure copy to the publish (deployment) folder tp the Raspberry Pi, specified folder
# replace "username" with your Raspberry Pi username, and "ip_address" with 
# the IP address of your Raspberry Pi.  This example assumes the deployment folder: ~/RTDMS_deployment
scp bin/Debug/net6.0/linux-arm/publish/* username@ip-address:~/RTDMS_deployment
```
<div style="background:lightblue;margin-left:1em;padding:1em;margin-top:.5em">
  <b> Note: </b>  You might want wish to setup your raspberry PI to use passwordless SSH, to enhance productivity:
  https://danidudas.medium.com/how-to-connect-to-raspberry-pi-via-ssh-without-password-using-ssh-keys-3abd782688a
</div>

