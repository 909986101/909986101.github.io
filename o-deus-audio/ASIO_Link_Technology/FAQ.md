# FAQ

## I can't hear anything

Follow the below steps:

1. Firstly, you must ensure that the ASIOVADPRO device is set up as the default windows audio device to capture all windows sounds (or set it as the output device for your favourite media player if you don't want to capture all windows sounds).

2. Next, you need to start an ASIO host application such as Ableton Live, Reason, FL, Reaper or Cubase but there are countless other ASIO applications.

3. Setup the ASIO Link Pro as the host programs ASIO device and, if it is the first time you have run it, pick the target ASIO driver you wish the ASIO Link Pro to output to.

4. Check the channels with the "Map" button in the "WDM Audio to ASIO OUT" section and you should see green in the V-meters when sound is played through ASIOVADPRO speakers.

5. The status should read "_Copied Audio Data_" and you should hear sound.

## I still can't hear anything

Follow the additional steps

1. If the status says "_No WDM audio stream_" it means nothing is playing to the ASIOVADPRO speaker out, play something in your favourite media player with output to the ASIOVADPRO speakers.

2. If the status says "_Sample rate mismatch_" it means you need to set the ASIOVADPRO windows device sample rate to the sample rate of the ASIO driver.

3. Make sure you have enabled ASIO channels you can actually hear in the appropriate matrix.

## I use ASIO4ALL

If you do use ASIO4ALL be sure not to enable the ASIOVADPRO Driver for the output/input device as this will not work (ASIO Link Pro mixes ASIOVADPRO audio into ASIO therefore it cannot be the selected device for ASIO4ALL).

![](../_media/26-1.jpg)  

## DAW specific

When using DAWs with ASIO Link there can be an issue with settings that offer to "unload" your ASIO driver when the application becomes inactive or loses focus.

It is best not to enable these features as ASIO Link Pro gives you access to all windows audio anyway!

If you enable these options be aware that the ASIO Link Pro driver may be shut down and restarted often making it hard to use the UI. It will also _cause problems running as a multi-client server_ as the driver will shut down causing clients to "disconnect".

### FL Studio

In FL Studio the setting is the **Auto Close** ASIO driver option (it is not enabled by default). Try not to enable it.

### Reaper

In Reaper the setting is **Close audio device when stopped and application is inactive**. Try not to enable it.

### I use Reason

In Reason the setting is **Play in background**. Try to keep it enabled as you want the driver to stay active even when focus is taken away from Reason.

### I use Wavelab or SoundForge

Wavelab and SoundForge both start and stop the ASIO driver so it is not wise to use it as a multi-client server at all. Always check the latest version as we do not check every version of these tools.

## I get a Failed IOCTL status from ASIOVADPRO

Make sure you fully uninstall a previous version before installing a new one. Try a complete uninstall and reinstall and it should then be fine. 

## What is this latency thing?

### ASIOVADPRO SPEAKERS / MIX Latency Adjustment

In the case of the ASIOVADPRO SPEAKERS IN rack, ASIOVADPRO MIX OUT rack, the latency is the time between the audio being written to, and the audio being read from the stream.

Windows writes audio into the ASIOVADPRO SPEAKERS and ASIO Link Pro reads audio behind it and the latency is the time delay. In the case of ASIOVADPRO MIX, windows is reading audio just after ASIO Link Pro writes audio and the latency is the time delay.

Usually you do not need to adjust this but you can reduce or add latency if required.

### NETWORK IN Latency Adjustment

The latency adjust in the NETWORK IN rack allows you to add latency to the network stream to stop drop outs. It is really dependent on the quality of the network connection whether this can be reduced to nearer 0. The range is the same as the stored buffer size which is 250ms of audio. In short, if it distorts, add some latency.

If you enable "Auto synchronise" the audio stream will use "adaptive resampling" to keep the incoming audio stream clock and local ASIO clock in time.

The value displayed in the latency box is a best estimate of the total latency from sender to receiver.

## I get distortion when mixing multiple channels

Make sure, when mixing multiple input channels into only a few channels, you reduce the volume of the multiple channels using the IN MIX or OUT MIX buttons. Hold the left mouse button and move the mouse up or down on the green circle volume control to adjust the volume. Try to make sure no red levels are visible in the level display. 

## WDM is running but status is "Not Active" with ASIO4ALL

Sometimes ASIO4ALL can have trouble getting the card if it was the default device before ASIO4ALL starts. The best way to work around this is to disable the card in playback devices before using the link. It doesn't always happen so you can just try a few times disabling certain inputs and outputs in ASIO4ALL.

## I see red channels with X

This means that the ASIO driver is not doing any audio processing at all. If this happens first try to reset the ASIO Link Pro driver (R button).

You can also try to restart the host application and possibly the computer and if that does not solve this issue then [contact us]().

![](../_media/28-1.jpg)  
