This guide covers setup and streaming using a smartphone as the camera, connected to a laptop

### Description
The camera connects to the laptop over WiFi. It streams to OBS Studio, which combines the audio from the Mirabox and the video from the camera and outputs the stream to YouTube, Zoom, etc.

# Installation
## 1. Laptop
1. Install [OBS Studio](https://obsproject.com/)
2. Install the [Droidcam OBS Plugin](https://www.dev47apps.com/obs/#plugin)
3. _On Mac_, install [4K Video Downloader](https://www.4kdownload.com/products/product-videodownloader) to get access to the hardware video encoder on your laptop.
4. Save the background [image file](https://raw.githubusercontent.com/rodneyswa/church-streaming/main/background-box.png)

## 2. Camera
1. Install the [DroidCam OBS app] (https://www.dev47apps.com/obs/#app)
    * Using an Android phone is better because you get the ability to zoom and change other camera settings from your laptop
2. Purchase the Pro upgrade to remove the screen logo and be able to user the remote controls

# Setup
1. Plug in your laptop to the ethernet cable
2. Turn on Mobile hotspot or Internet Sharing
    * _On Mac:_
        * Go to System Preferences
        * Select Sharing
        * Select Internet Sharing, and in "To computers using:" select Wi-Fi
        * Set the Wi-Fi Options
            * Strongly prefer using a 5Ghz channel (above 11)
            * Set a password
        * Click the Internet Sharing checkbox. If this is the first time and it does not turn on, unset the checkbox and reboot your laptop. Then go back and click it to "On" and it should work
    * _On Windows:_
        * ?
3. Connect your phone to your laptop's WiFi. Using this WiFi results in lower latency, because the stream goes direct to the laptop instead of an access point which then relays the stream to the laptop.
4. Run the DroidCam OBSapp
5. Open OBS Studio on your laptop
    1. Go to Settings. Click Video on the left
        1. Set the Base Canvas to 1920x1080
        2. Set the Output (Scaled) to 1920x1080
        3. Set the Downscale Filter to Lanczos
        4. Set FPS to 30
    2. Click on Scene, then add a Source.
        1. Select DroidCam OBS. Set the Resolution to 1920x1080. Enter the WiFi IP to the address that the camera app shows. Typically 192.168.2.1
        2. Click Activate. Video should appear. Click OK
    3. Add another Source for audio
        1. Select Audio Input Capture. Name it Chapel Audio
        2. For the device select Mirabox Video Capture
    4. Go to Settings. Click Audio on the left
        1. Set rate and channel to 44.1 kHz and Mono.
        2. Set Mic - all Global Audio devices to disabled
        3. Click OK. You may need to restart OBS when changing to Mono
    5. Go to Settings. Click Output on the left
        1. Select Output Mode: Advanced
        2. Select the Streaming tab
            1. Select the Apple VT H264 Hardware Encoder (highly preferred), or else 'x264'
            2. Set Bitrate to 3000 Kbps
            3. Keyframe Interval: 3
            4. Profile: high
        3. Select the Audio tab
            1. Set Track 1 Audio Bitrate to 128
     6. Select Stream on the left
     7. Select:
        1. Service: YouTube - RTMP
        1. Server: Primary YouTube ingest server
        1. Stream key: <Click on Get Stream Key to go to [YouTube.com/live_dashboard](https://YouTube.com/live_dashboard). Copy the '1080p Key' and paste it here
        2. Click OK

# Start the Stream
1. Go to [YouTube.com/live_dashboard](https://YouTube.com/live_dashboard) in your browser
2. In OBS click Start Streaming

# Stop the Stream
1. In your browser click on End Stream at the top right
2. In OBS click Stop Streaming

