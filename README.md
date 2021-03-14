This guide covers setup and streaming using a smartphone as the camera, connected to a laptop, for a higher quality image instead of using the 480p camera installed in the building.

# Overview
Phone provides the video. 
Mirabox provides the audio. 
Laptop uses OBS to put the audio and video together and stream it. 

The phone (aka camera) connects to the streaming laptop over WiFi using the Droidcam app. The video streams to OBS Studio, which combines the audio from the Mirabox and the video from the camera and outputs the stream to YouTube, Zoom, etc.

# Installation
### 1. Laptop
1. Install [OBS Studio](https://obsproject.com/)
2. Install the [Droidcam OBS Plugin](https://www.dev47apps.com/obs/#plugin) NOTE! This is not the same as the DroidCam OBS app. You need to install both. 
3. _On Mac_, install [4K Video Downloader](https://www.4kdownload.com/products/product-videodownloader) to get access to the h.264 hardware video encoder on your laptop. The hardware encoder use much less CPU usage.
4. Save the background [image file](https://raw.githubusercontent.com/rodneyswa/church-streaming/main/background-box.png) if you want to add captions.

### 2. Phone
1. Install the [DroidCam OBS app](https://www.dev47apps.com/obs/#app) on your phone. App is available for both Android and iOS.
    * Using an Android phone is better because you get Remote Control
2. Purchase the Pro upgrade to remove the screen logo and be able to use the Remote Control - which allows you to zoom and lighten/darken the video from your laptop.

# Setup
1. Plug in your laptop to the ethernet cable
2. Turn on Mobile Hotspot or _for Mac_, Internet Sharing
    * _On Mac:_
        * Go to System Preferences
        * Select Sharing
        * Select Internet Sharing from the service menu on the left. 
        * In the 'Share your connection from' dropdown, select Ethernet/LAN or USB if you use USB to Ethernet adaptor.
        * In the 'To computers using' menu, select Wi-Fi
        * Set the Wi-Fi Options
            * Strongly prefer using a 5Ghz channel (above 11)
            * Set a password
        * Click the Internet Sharing checkbox to turn it on. If this is the first time and it does not actually turn on, unset the checkbox and reboot your laptop. Then go back and click checkbox to "On" and it should turn on.
        * 
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
## Setup for Titles
Titles, or captions help the ward get to know each other.
This section creates another 'Scene' which overlays titles on the previous scene's audio an video feed.
1. Create another Scene by selecting the '+' at the bottom ofthe Scenes pane. Name it 'Scene+Title'
2. Select the new Scene.
3. In Sources, click '+' and select Scene. Select "Add Existing' to add your previous 'Scene' to this scene.
4. In Sources, click '+' and add an Image. Select the downloaded [background-box.png](https://raw.githubusercontent.com/rodneyswa/church-streaming/main/background-box.png) image. Rename it 'Background'
5. In Sources, click '+', add a 'Text (FreeType 2)'
    1. Select a font and size - Helvetica (size 48) or Myriad Pro (size 64). Click OK
    2. Type some text such as 'Bishop Bill Hatch' with 'Bishop' on the second line
    3. Scroll down and select checkbox Drop Shadow. Hit OK
    4. Rename it to just 'Text'
6. Make sure your Sources are in this order:
    1. Text
    2. Background
    3. Scene
7. Adjust location in the window by selecting Text and Background and moving them to the lower left. The Background image should extend 60% across the screen. Text should be indented a little from the left side and a little from the bottom
8. In the Scene Transitions pane, set Duration to 800 ms
### How to use
1. Click on Studio Mode. The right 'Program' view is what you are streaming. The left is a Preview. Clicking Transition at the top center switches the two.
2. Rule: Never edit a title while you are streaming titles, because everyone will see you type each character. Instead: 
    1. Transition to the scene without titles
    2. Select the Title scene and Text source. Click Properties and edit the title (I put all Name and titles in a text file ahead of time so I can just copy-paste)
    3. Press Transition to switch to streaming the new title

# Operations
Mount your phone in the microphone stand which has the phone holder/clamp on it. The top edge is spring loaded. Just pull up and insert camera.
Connect your camera to power with a USB cord, so it doesn't go to sleep. I went in to Developer Options and set Stay Awake.

## Start the Stream
1. Go to [YouTube.com/live_dashboard](https://YouTube.com/live_dashboard) in your browser
2. Select Normal Latency at the bottom
3. In OBS click Start Streaming

## Stop the Stream
1. In your browser click on End Stream at the top right
2. In OBS click Stop Streaming
3. Delete the completed livestream. Go to Studio > Content > Live and delete the live stream.

