# Using ASIO Link Pro

Using the ASIO Link Pro can seem daunting at first but after a while you can easily send audio to friends, loopback audio to other drivers, send audio from DAW – DAW.

_'Anything is possible with ASIO Link Pro'_

## ASIO Link Pro User Interface

The UI consists of two parts

1. The settings and help bar section (top part)
2. The channel racks (lower, larger part)

![](../_media/11-1.jpg)  
_ASIO Link Pro UI sections 1 + 2_

## Settings and Help Bar

There are many settings and buttons available in the top part of the ASIO Link Pro UI. They are described in [Top Settings]() in detail.

Just below those is the help bar. When you "mouse over" a control the help bar will give a brief summary of what that control does. Below, it is giving a help tip on the help bar itself.

![](../_media/11-2.jpg)  
Settings and Help Bar

## Channel Racks and Channel Connections

In the UI section 2 you can see seven sections, each containing a horizontal row of channels. They are categorised into 3 types

### Mix Racks

There are 2 mix racks

- ASIO HOST IN MIX 
- ASIO DRIVER OUT MIX

### Input Racks

There are 3 input racks

- ASIOVADPRO SPEAKERS IN 
- ASIO DRIVER IN 
- NETWORK IN

### Output Racks

There are 2 output racks

- ASIOVADPRO MIX OUT 
- NETWORK OUT

All Input racks and Output racks have an **IN MIX** button and **OUT MIX** button which allows you to control the routings and volume of each channel to the ASIO HOST IN MIX and ASIO DRIVER OUT MIX. They also have a volume control.

The ASIO HOST IN MIX and ASIO DRIVER OUT MIX are known collectively as the MIX racks.

These are the main audio bus racks for ASIO Link Pro. Audio can be mixed both to and from both of these racks. They are both input and output racks, hence the term MIX RACK.

### Channel Connections

Depending on the **Show audio flow** setting (see [Top Settings]()) you can see either some lines or all lines connecting channels on racks. These are called channel connections and can be created by drag-dropping channels as described [below]().

## MIX RACKS

### ASIO HOST IN MIX

![](../_media/12-1.jpg)  

This rack is the PRE-MIX for your ASIO host programs ASIO input channels. All audio mixed into ASIO HOST IN MIX will appear in your ASIO host.

The **X** button clears all routings.

### ASIO DRIVER OUT MIX

![](../_media/12-2.jpg)  

This rack is the PRE-MIX for your ASIO driver output. This is where the audio processing has been finished and everything has been mixed in ready to send to the ASIO driver or multi-client server (see [Multi-client Mode]()).

All audio sent here, including your ASIO host program output, which is always mixed in, is sent to the ASIO driver or multi-client server.

The **X** button clears all routings.

## INPUT RACKS

### ASIOVADPRO SPEAKERS IN

![](../_media/13-1.jpg)  

WDM meets ASIO with ASIOVADPRO SPEAKERS IN. Any audio played to the ASIOVADPRO Speakers 01 – 04 shall appear on this rack as an input to ASIO HOST IN MIX and/or ASIO DRIVER OUT MIX. As shown above, the channels are connected to the ASIO HOST IN MIX and are being processed by the HOST as ASIO inputs.

Each ASIOVADPRO device has WDM specific controls

- Latency The latency wheel enables adjusting the WDM stream latency. It is fine to leave this at 0.0ms. It also displays the current stream latency.  
![](../_media/13-2.jpg)  

- Status Below the latency wheel there is a text box displaying the ASIOVADPRO device status for each device.  
![](../_media/13-3.jpg)

If the device is unavailable, or there is an error, channels will appear red with an X over the channel number.

By default, when you first start/select ASIO Link Pro in a new host program, the routings 1-1 and 2-2 shall be enabled by default to the ASIO DRIVER OUT MIX.

### ASIO DRIVER IN

![](../_media/13-4.jpg)  

These are the actual real ASIO driver inputs like microphone and line in etc.

If you have an input plugged into your soundcard then you can send it to ASIO HOST IN MIX and/or ASIO DRIVER OUT MIX.

By default, when you first start/select ASIO Link Pro in a new host program, the routings 1-1 and 2-2 shall be enabled by default to the ASIO HOST IN MIX.

### NETWORK IN

![](../_media/13-5.jpg)

Receive up to 16 channels of audio over the network from another machine that is running another instance of the ASIO Link Pro driver (see [Networking]()).

Notice this rack has some networking specific controls

- **Latency** which allows you to move the stream back from the incoming stream to leave enough latency to avoid drop outs. It is up to the user to set this value right so no distortion can be heard. The latency on the stream is to left in the square brackets and network jitter on the right in the square brackets. The network jitter value will give you a rough idea of what latency should be selected, it shows the maximum variance in received packet delay.  
![](../_media/14-1.jpg)  

- ![](../_media/14-2.jpg) **R** Resets the network latency to the value in the latency wheel

- **Local IP** is the IP address and port of the current machine running ASIO Link Pro. An example is **192.168.1.101:5060**

- **Auto synchronise** keeps the incoming stream in sync with the host program by adaptively adjusting the incoming sample rate so the streaming does not get out of synchronisation.

- **Enable connection** when checked, enables the connection if there are any channels connected to ASIO HOST IN MIX and/or ASIO DRIVER OUT MIX

## OUTPUT RACKS

### ASIOVADPRO MIX OUT

![](../_media/14-3.jpg)  

ASIO meets WDM with ASIOVADPRO MIX OUT. Stream DAW audio over any application that can record WDM, MME, WASAPI or any other WDM based audio stream.

The audio output here is recordable by any normal windows audio application (e.g. sound recorder). If any mappings/connections are enabled, the audio on either ASIO HOST IN MIX and/or ASIO DRIVER OUT MIX will be sent to the ASIOVADPRO Mix device(s).

Each ASIOVADPRO device has WDM specific controls

- **Latency** The latency wheel enables adjusting the WDM stream latency. It is fine to leave this at 25.0ms. It also displays the current stream latency  
![](../_media/14-4.jpg)  

- **Status** Below the latency wheel there is a text box displaying the ASIOVADPRO device status for each device  
![](../_media/14-5.jpg)  

If the device is unavailable, or there is an error, channels will appear red with an X over the channel number.

By default, when you first start/select ASIO Link Pro in a new host program, the routings 1-1 and 2-2 shall be enabled by default from the ASIO DRIVER OUT MIX.

_Since most windows applications can only open recording devices in stereo, you can down mix surround sound to stereo by adjusting the mappings appropriately._

### NETWORK OUT

![](../_media/15-1.jpg)  

NETWORK OUT can send audio over the network to another machine that is running another instance of the ASIO Link Pro driver (see [Networking]()).

Notice this rack has some networking specific controls

- **Format** sets the wave audio format to be sent over the network. You can set the sample rate and bit depth. It is best to set both sender and receiver machines to the same sample rate and ASIO buffer size and set the same format in this control. This ensures minimal re sampling needs to take place making the sound quality the best it can be.

- **Remote IP** is the host IP address and port of the machine you wish to send audio to, an example address is **127.0.0.1**

- **Enable connection** when checked, enables the connection if there are any channels connected to ASIO HOST IN MIX and/or ASIO DRIVER OUT MIX

## Connecting Inputs and Outputs

The ASIO Link Pro UI allows two ways to connect channels from audio inputs to audio outputs.

### Method 1 – Drag Drop Channels

If you click and hold the mouse over a channel, then drag the mouse, channels you can connect to become highlighted. All you need to do is drop the channel onto a highlighted channel and a connection is made.

<div style="display: grid; grid-template-columns: 3fr 0.75fr 6.25fr;">
  <div>
  
  ![](../_media/15-2.jpg)
  </div>
  <div></div>
  <div>Dragging channel 1 from ASIOVADPRO SPEAKERS IN to ASIO HOST IN MIX channel 1 connects the audio input to the MIX RACK. EASY!!! </div>
</div>

_Drag-Drop Channels_


TIP - If you mouse-over a channel connection it will become selected and will be displayed with a solid colour if your mouse is over either channel it is connected to. If you now click and release the left mouse button, the connection(s) will be deleted.

_BE CAREFUL NOT TO ACCIDENTALLY DELETE CONNECTIONS!_

### Method 2 – Mapping Buttons (IN MAP X 1-1 or OUT MAP X 1-1)

IN and OUT racks each have **IN MIX**, **X** and 1-1 buttons and also **OUT MIX**, **X** and **1-1** buttons.

![](../_media/16-1.jpg)  
_IN MIX, X, 1-1 and OUT MIX, X, 1-1 buttons_

### Quick Mapping

The **X** buttons clear all connections to the IN MIX (left) or OUT MIX (right).

The **1-1** buttons set up 1 - 1, 2 - 2, 3 - 3, 4 – 4, and so on, connections to the ASIO HOST IN MIX (left) or the ASIO DRIVER OUT MIX (right).

### The Mapping Window

If you click on **IN MIX** or **OUT MIX** you will bring up the _Mapping Window._

The mapping window allows exact configuration of audio routing from an audio input or output to either the ASIO HOST IN MIX or ASIO DRIVER OUT MIX racks.

In the below image, the mapping window matrix has 4 x 8 channels (from ASIOVADPRO SPEAKERS IN) going down and 8 channels (from ASIO HOST IN MIX) going across.

<div style="display: grid; grid-template-columns: 2fr 0.75fr 7.25fr">
  <div>
  
  ![](../_media/16-2.jpg)
  </div>
  <div></div>
  <div>
    <p>In the Mapping window you can assign channels to ASIO HOST IN MIX or ASIO DRIVER OUT MIX.</p>
    <p>In the left the routing is to ASIO HOST IN MIX and this window is available for all INPUT and OUTPUT racks. </p>
    <p>NOTE – If you subsequently "drag-drop channels" or use "quick mapping" then the volume information will be set to the default of 0dB. It is your choice to use either "drag- dropping", "quick-mapping" or the "mapping window". </p>
  </div>
</div>

_Mapping window_

It is normal to map channels 1 – 1, 2 – 2, 3 – 3 etc. This is the standard way to set up for the input to be sent to the output. The volume of each routing is adjustable between minus infinity dB (no volume) and 6.02dB. The default value is 0dB.

It is possible to mix multiple channels into single channels and vice versa for down mixing or up mixing channels or converting mono to stereo etc.

## Top Settings

![](../_media/17-1.jpg)  

### Profiles

**Profile 1 - 8** – This allows you to select a profile slot which stores routing settings. If you save or load a routing profile, the profile slot will take on the name of the file.

**Load** – Loads routing settings from disk to the current selected profile slot

**Save** – Saves the current routing settings to disk and to the current selected profile slot

### Options

**Record to file** – You can send up to 8 channels of audio out to a FLAC file by enabling this (see [Recording to FLAC file]())

**Enable multi-clients** – This allows you to run more than one instance of ASIO Link Pro for multi-client usage (see [Multi-client Mode]())

**Show audio flow** – You can see all rack connections when this is enabled. It makes it easier to see where audio is going but can get cluttered when many routings are active. If not enabled, you can only see the audio connections if you have the mouse over rack the connection is connected to.

**Show performance** – This allows you to see performance metrics. It shows the total time in microseconds taken for audio processing, the host application time and ASIO Link Pro times.

![](../_media/17-2.jpg)  

**Show max values** – Shows the maximum values over time for each performance display value.

### Buttons

**R** – Request an ASIO driver reset from the host application

**Pick driver** – Picks another ASIO driver to host (requires host restart or driver reload)

**ASIO CPanel** – Opens the hosted drivers ASIO control panel

**WinMM CPanel** – Opens the Windows multimedia control panel

**About** – Opens an about box showing copyright information

**Enter product key** – Pops up a dialog to enter your product key or purchase ASIO Link Pro ([Enter a Product Key])

**Unregister ASIO Link** – Remove the license to ASIO Link Pro from this machine ([Transfer Your License])

## Recording to FLAC file

The ASIO Link Pro can record the first 8 ASIO output channels to a FLAC file!

When you enable this a dialog shall pop up to pick a folder and once selected a file will be created with a name in the following format "asiolink-2014-12- 22_20-06-59.flac". The timestamp is the date-time recording started.

FLAC files can take up a lot of disk space. Especially 8 channel ones.

|||
|:--|:--|
|![](../_media/18-1.jpg) |![](../_media/18-2.jpg)|

Once a folder is selected, every time ASIO Link Pro starts, a new FLAC file is created. 

## Running Multiple Instances

See below regarding multi-client support but if you run a second instance of ASIO Link Pro - without enabling multi-client mode in the first instance - you will not have access to the WDM audio as that is already used by the first instance.

However, if you have more than one ASIO soundcard, you can use this to route audio using loop networking from one application to another and use two ASIO soundcards at once!

So if you start say, ASIO Link Pro with driver one normally and disable multi clients, you can then load up another host program and connect to a different ASIO driver. This will allow you to now send audio via the networking from the second instance to the first instance or vice versa.

## Multi-client Mode

The ASIO Link Pro can run in multi-client server mode allowing more than one application to share one ASIO driver. In order to do this you should run a "server" ASIO Link Pro instance and enable the Enable multi-clients check box.

![](../_media/19-1.jpg)  
_Enabling multi -client Mode_

Now, when you run an application that uses ASIO Link Pro it will use the inbuilt _ASIO Link Multiclient_ ASIO driver.

Using the _ASIO Link Multiclient_ you can send audio from more than one application to your ASIO Drivers sound output or the ASIO inputs of the server application.

You can run up to **25** instances of ASIO Link Pro in anything from standalone VSTs to DAWs.

To capture output to the ASIO inputs of your server application, enable the **Route to ASIO IN** check box in the client application.

![](../_media/19-2.jpg)  
_Routing multi-client output to ASIO Inputs of the multi-client server host application_

In multi-client mode you can still capture ASIOVADPRO SPEAKERS IN and ASIO DRIVER IN and you can also send audio to the ASIOVADPRO MIX OUT rack. One thing to note is that all the audio is going to the server instance so you need to be careful not to overload the ASIOVADPRO MIX OUT!

_AND, REMEMBER, YOU ALWAYS HAVE ACCESS TO NETWORKING!_  
_NETWORKING CAN ROUTE AUDIO ANYWHERE!_

## Networking

### Network IP address and port format

When entering the Local or Remote IP addresses for NETWORK IN and NETWORK OUT respectively, you can append a port to it with a colon. If you don't it will default to port 5050. An example address is the loopback address **127.0.0.1:5050**

### Network port forwarding and obtaining your IP address

To obtain your IP address, run a command prompt (search for cmd.exe) and type "ipconfig.exe" and press enter and you will see something like this:

![](../_media/20-1.jpg)  
_"ipconfig.exe" output_

IP address of your machine is not necessarily this on the internet, but for routing over the LAN, this is the address you want. To connect on the internet, often you have to enable traffic on port 5050 (or whatever port you select) with your ISP and with your firewall. You also have to explicitly set the IP address in the adapter settings (right click the network icon in the system tray to get to Local Area Connection Properties)

|||
|:--|:--|
|![](../_media/20-2.jpg) |![](../_media/20-3.jpg) |

_Network adapter settings/IPv4 settings_

Now to get your actual real IP address and to check that your port is open, do a google for online port checker and use it to

- Find your "real" internet address 
- Check whether access to the port is enabled (default is 5050)

After this it should allow others to connect to your Link driver. You can send and receive audio from your own IP address and you can do some rather cool things with networking!

See the examples in [Send DAW ASIO output to another DAW ASIO input and Receive audio into your host program from the network or LAN]().

### Additional NETWORK IN and NETWORK OUT Racks

You can enable a second NETWORK IN and NETWORK OUT rack if you enable the **Enable second NETWORK IN/OUT** check box in the [ASIO Link Pro Tool](). You can now send/receive audio from two other machines running ASIO Link Pro!

_Do not underestimate the power of networking!_

## Audio Loopback via the Optional LOOPER Racks

### Loopback racks

There are two racks that can be enabled by enabling the **Enable LOOPER loopback racks** check box in the [ASIO Link Pro Tool]. Once enabled the UI shall add two extra racks and they are described below

### LOOPER OUT

![](../_media/21-1.jpg)  

You can send audio to this rack to and it will be looped back through the LOOPER IN rack

### LOOPER IN

![](../_media/21-2.jpg)  

Audio sent to the LOOPER OUT rack will be available on this rack. There will be one audio buffer of latency on audio sent via the LOOPER OUT and LOOPER IN mechanism.

You can also send audio to LOOPER OUT and receive audio from LOOPER IN in [Multi-client Mode]. Note, when in this mode be careful not send audio to the LOOPER OUT that is already being sent to LOOPER OUT in the main server instance of ASIO Link Pro.
