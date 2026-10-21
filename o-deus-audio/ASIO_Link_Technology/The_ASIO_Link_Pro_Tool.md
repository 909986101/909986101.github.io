# The ASIO Link Pro Tool

This is both a configuration tool and a simple ASIO host application to allow configuring and testing the ASIO Link Pro. It can be very helpful to find and diagnose problems as you are in control of all the ASIO settings.

It can also clear all your default settings for host applications. This is like starting with a fresh install if you wish to start anew.

## Using the ASIO Link Pro Tool

![](../_media/23-1.jpg)  
_ASIO Link Pro Tool UI_

## ASIO Link Pro Tool Functions

### ASIO Settings

**Sample rate** – The ASIO sample rate to set. 'ASIO preferred'.is the default value and it uses the ASIO driver's default sample rate.

**Buffer size** – The ASIO buffer size to try to set in the driver. If low latency is desirable (lower size means lower latency) then try to set this as low as you can but if set too low, audio can distort. 'ASIO Preferred' is the default value and will use the ASIO driver's preferred buffer size.

**Channels IN/OUT** – Choose the number of input and output channels.

**Init ASIO** – Initialises, but does not start, the ASIO Link Pro driver.

**START ASIO** – Starts the ASIO Link Pro driver's audio processing and you can use the test tone to test your ASIO driver.

**Stop ASIO** – This stops the ASIO Link Pro driver.

**ASIO CPanel** – Launches the ASIO driver's control panel.

**Test tone** – Plays a 440Hz test tone to all enabled ASIO output channels.

**Send IN to OUT** – ASIO Link Pro Tool will route audio from ASIO input to the ASIO output. This option is still included but you can route audio in any way you wish in the ASIO Link Pro driver.

### Tool Settings

**Start minimised and START ASIO** – When enabled, the ASIO Link Pro Tool will start minimised to the system tray and automatically start the ASIO Link Pro. This can be useful if you wish to start ASIO Link Pro with windows.

**Start with windows** – When enabled, the ASIO Link Pro Tool will start with windows. Usually you would also enable the Start minimised and START ASIO option too to automatically start ASIO.

### ASIO Link Settings

**Start ASIO Link Pro minimised** – Start the ASIO Link Pro driver minimised to the system tray so the UI does not pop up till the tray icon is clicked.

**Do not check for updates** – ASIO Link Pro will no longer prompt you if you an update is available

**Allow ASIO Link Pro to get focus** – Allows the ASIO Link Pro to become the activated/focused window. The reason this is not enabled by default is that the ASIO Link Pro can take focus away from host applications or DAWs that auto- close the ASIO driver! When this happens, ASIO Link Pro gets "closed" by the host. Be careful if you enable this and read the FAQ below.

**Enable LOOPER loopback racks** – ASIO Link Pro will show two additional racks named LOOPER IN and LOOPER OUT to allow sending audio back to for use as an input.

**Enable second NETWORK IN/OUT** – ASIO Link Pro will now show two additional networking racks named NETWORK IN 2 and NETWORK OUT 2 to allow sending/receiving audio from another machine.

### ASIOVADPRO (WDM) settings

**WDM test tone** – Plays a stereo 880Hz test tone to the first ASIOVADPRO speakers.

**WinMM CPanel** – Launches the windows multimedia control panel.

**Use strict ASIO clock** – The ASIOVADPRO WDM driver normally uses smoothing to average out the ASIO clock time and its own DPC clock time. When strict ASIO clock is enabled ASIOVADPRO uses only the ASIO clock.

**Auto-set audio wave format** – The ASIOVADPRO sample rate and bit format will be automatically set when ASIO Link Pro is in use (not available in Windows XP).

**Auto-set as default audio device** – ASIOVADPRO will be automatically set as the default audio playback and recording devices when in ASIO Link Pro is in use (not available in Windows XP).

**Allow 32 bit PCM format** – ASIOVADPRO will use 32 bit wave format if the ASIO driver is using 32bit wave format. This setting requires Auto-set ASIOVADPRO wave format to be enabled (not available in Windows XP).

### Miscellaneous

**About** – Shows an "About" dialog box.

**Reset settings** – Clears all saved settings for ASIO Link Pro and ASIO Link Pro Tool.

**Exit** – Exits the ASIO Link Pro Tool.
