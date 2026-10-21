# Sample Configurations

## Mix WDM playback into host application input

By enabling connections from ASIOVADPRO SPEAKERS IN to ASIO HOST IN MIX you can bring WDM audio into your host applications ASIO input channels.

You can pull audio from any windows audio source that is using WASAPI, MME or DirectSound.

You can quickly achieve this by clicking the "**1-1**" button shown below.

![](../_media/29-1.jpg)  
_Send WDM playback to ASIO input_

### Uses

- Bring WDM WASAPI, MME or DirectSound audio into your DAW or ASIO application 
- Record windows WDM application audio into your ASIO host

## Send ASIO output to WDM recording devices

By enabling connections from ASIO DRIVER OUT MIX to ASIOVADPRO MIX OUT you can send your ASIO output to the ASIOVADPRO WDM recording devices.

You can push audio to any windows audio application that is using WASAPI, MME or DirectSound.

To use the output simply select the ASIOVADPRO MIX 01-04 (or 01-16) in your screen casting or recording software.

You can quickly achieve this by clicking the "**1-1**" button shown below.

![](../_media/30-1.jpg)  
_Send ASIO output to WDM recording devices_

### Uses

- Send ASIO audio to any WASAPI, MME or DirectSound application 
- Capture DAW audio into screen casting applications

## Send DAW ASIO output to another DAW ASIO input

To achieve this you need to use multi-client mode.

First, start the server DAW that will receive the audio input from another DAW. Below I have started Ableton Live and selected the ASIO Link Pro ASIO driver and I made sure that "**Enable multi-clients**" is enabled. Also, enable all the ASIO input and output channels you need.

![](../_media/31-1.jpg)  
_Start the server DAW_

Next, start the DAW that will send audio to Ableton Live. I have started FL Studio and made sure I enabled the "**Route to ASIO in**" option to send audio to Ableton Live ASIO inputs. Note I have selected channels 3+4 for output so that audio output from FL Studio appears on Ableton Live ASIO input channels 3 + 4.

![](../_media/31-2.jpg)  
_Start the DAW to send audio from_

### Uses

- Send ASIO audio output from one application to another applications ASIO inputs

## Send audio over IP on the network or LAN

By enabling connections from ASIO DRIVER OUT MIX to NETWORK OUT you can send audio over IP.

You can quickly achieve this by clicking the "**1-1**" button.

Next, enter the Remote IP address of the target machine that is running ASIO Link Pro with NETWORK IN enabled so it can receive the audio.

NOTE: You need to check the "**Enable connection**" check box to start sending audio.

![](../_media/32-1.jpg)  
_Send audio over IP_

### Uses

- Send audio to another machine on the network running ASIO Link Pro 
- Set up full-duplex audio send and receive to share ideas with another musician in real time 
- Use loopback IP (127.0.0.1) to send audio to the same machine 
- Combine with [Multi-client Mode]() to receive audio from more than one machine

## Receive audio into your host program from the network or LAN

By enabling connections from NETWORK IN to ASIO HOST IN MIX you can receive audio over IP.

You can quickly achieve this by clicking the "**1-1**" button and entering the IP address of the local machine running ASIO Link Pro so it can listen for incoming connections.

NOTE: You need to check the "**Enable connection**" check box to start sending audio.

![](../_media/33-1.jpg)  
_Receive audio over IP_

### Uses

- Receive audio from another machine 
- Set up full-duplex audio send and receive audio to share ideas with another musician in real time 
- It is possible to use the loopback address (127.0.0.1) to receive audio sent from the same machine 
- Combine with Multi-client Mode to receive audio from more than one machine
