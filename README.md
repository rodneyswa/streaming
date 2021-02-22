This guide covers setup and streaming using a smartphone as the camera, connected to a laptop, for a higher quality image instead of using the 480p camera installed in the building.

### Description
The camera connects to the laptop over WiFi. It streams to OBS Studio, which combines the audio from the Mirabox and the video from the camera and outputs the stream to YouTube, Zoom, etc.

# Installation
### 1. Laptop
1. Install [OBS Studio](https://obsproject.com/)
2. Install the [Droidcam OBS Plugin](https://www.dev47apps.com/obs/#plugin)
3. _On Mac_, install [4K Video Downloader](https://www.4kdownload.com/products/product-videodownloader) to get access to the h.264 hardware video encoder on your laptop. The hardware encoder use much less CPU usage.
4. Save the background [image file](https://raw.githubusercontent.com/rodneyswa/church-streaming/main/background-box.png) if you want to add captions.

### 2. Phone
1. Install the [DroidCam OBS app](https://www.dev47apps.com/obs/#app) on your phone
    * Using an Android phone is better because you get Remote Control
2. Purchase the Pro upgrade to remove the screen logo and be able to use the Remote Control - which allows you to zoom and lighten/darken the video from your laptop.

# Setup
1. Plug in your laptop to the ethernet cable
2. Turn on Mobile Hotspot or _for Mac_, Internet Sharing
    * _On Mac:_
        * Go to System Preferences
        * Select Sharing
        * Select Internet Sharing, and in "To computers using:" select Wi-Fi
        * Set the Wi-Fi Options
            * Strongly prefer using a 5Ghz channel (above 11)
            * Set a password
        * Click the Internet Sharing checkbox to turn it on. If this is the first time and it does not actually turn on, unset the checkbox and reboot your laptop. Then go back and click checkbox to "On" and it should turn on.
    * _On Windows:_
        * ?
3. Connect your phone to your laptop's WiFi. Using this WiFi results in lower latency, because the stream goes direct to the laptop instead of an access point which then relays the stream to the laptop. Or worse, over WiFi twice.
4. Run the DroidCam OBS app on your phone. It shows the IP address to add to OBS Studio
5. Open OBS Studio on your laptop
    1. Go to Settings. Click Video on the left
        1. Set the Base Canvas to 1920x1080
        2. Set the Output (Scaled) to 1920x1080
        3. Set the Downscale Filter to Lanczos
        4. Set FPS to 30
    2. Click on Scene, then add a Source.
        1. Select DroidCam OBS. Set the Resolution to 1920x1080. Enter the WiFi IP to the address that the camera app shows. Typically 192.168.2.1
        2. Click Activate. Video should appear. Click OK
    3. Add another Source - for audio
        1. Select Audio Input Capture. Name it Chapel Audio
        2. For the device select Mirabox Video Capture. This captures only the audio from the chapel.
    4. Go to Settings. Click Audio on the left
        1. Set rate and channel to 44.1 kHz and Mono.
        2. Set Mic - all Global Audio devices to disabled
        3. Click OK. You may need to restart OBS when changing to Mono
    5. Go to Settings. Click Output on the left
        1. Select Output Mode: Advanced
        2. Select the Streaming tab
            1. Select the _for Mac_ Apple VT H264 Hardware Encoder (highly preferred), or else 'x264'
            2. Set Bitrate to 3000 Kbps. Max rate for this is 6000 kbps.
                * If Bishop Cannon uses the building's internet for his Youth Council meeting (at the same as our meeting), you can't stream at 6,000.
            4. Keyframe Interval: 3
            5. Profile: high
        3. Select the Audio tab
            1. Set Track 1 Audio Bitrate to 128 (can set all tracks to 128)
     6. Select Stream on the left
        1. Select:
            1. Service: YouTube - RTMP
            2. Server: Primary YouTube ingest server
            3. Stream key: <Click on Get Stream Key to go to [YouTube.com/live_dashboard](https://YouTube.com/live_dashboard). Copy the '1080p Key' and paste it here>
     7. Click OK
## Setup for Captions
Captions are good for helping the ward get to know each other.
* to be completed...

# Operations
Mount your phone in the microphone stand which has the phone holder/clamp on it. The top edge is spring loaded. Just pull up and insert camera.
Connect your camera to power with a USB cord, so it doesn't go to sleep. I went in to Developer Options and set Stay Awake.

## Start the Stream
1. Go to [YouTube.com/live_dashboard](https://YouTube.com/live_dashboard) in your browser
2. In OBS click Start Streaming

## Stop the Stream
1. In your browser click on End Stream at the top right
2. In OBS click Stop Streaming
3. Delete the completed livestream. Go to Studio > Content > Live and delete the live stream.

