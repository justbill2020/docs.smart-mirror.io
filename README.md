# Smart Mirror

[![Join the chat at https://gitter.im/evancohen/smart-mirror](https://badges.gitter.im/evancohen/smart-mirror.svg)](https://gitter.im/evancohen/smart-mirror?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This project was inspired by [HomeMirror](https://github.com/HannahMitt/HomeMirror) and Michael Teeuw's [Magic Mirror](http://michaelteeuw.nl/tagged/magicmirror). It uses [annyang](https://github.com/TalAter/annyang) for voice interactivity, [electron](http://electron.atom.io/) to make it cross platform, and integrates with Philips Hue. It is my own take on what a "smart mirror" can be.

[See it in action (Video)](https://www.youtube.com/watch?v=PDIbhV8Nvq8)

#### Why start from scratch?
Starting from scratch was less about other projects not being good enough and more about my own learning experience. While I did get a lot of inspiration from other projects I really wanted to see how much further I could take things.

#### Gitter:
A live chat to get help and discuss mirror related issues: https://gitter.im/evancohen/smart-mirror. Usually there are a few folks hanging around in the lobby, but if there arent you are probubly better off [filing an issue](https://github.com/evancohen/smart-mirror/issues/new).

### Getting Started
#### Hardware Components
- Raspberry Pi 2** (Only the Raspberry Pi 2 is compatible with the mirror ATM) 
- USB Microphone (Or Webcam w/ microphone)
- Monitor (with the bezel removed)
- Mirror Pane (aka Observation Glass/Two way mirror)
- Philips Hue lights

** Also compatible with other Linux, Windows, and OSX devices. See the `cordova` branch for Android and iOS compatibility.

#### How to set up the Raspberry Pi

##### 1. Raspberry Pi 2
Buy a Raspberry Pi 2 if you haven't already [(Click here.)] (https://www.raspberrypi.org/products/raspberry-pi-2-model-b/) 

##### 2. Power supply
You will need a power supply in order to make the Raspberry PI 2 work.
Be careful when buying a power supply and make sure that it is designed to work with the Raspberry PI 2 otherwise you might fry the board. It should have a minimum of 2A. You can buy original power supplies [here.](https://www.raspberrypi.org/products/universal-power-supply/)

##### 3. Micro SD card 
You will need a micro SD card for running the operating system on the Raspberry PI and for storage space. Any brand of SD card will do, just make sure that is has minimum <strong>8GB</strong> of storage.

##### 4. WIFI dongle
It is strongly recommended that you buy a WIFI dongle, so your Pi does not have to be connected to an Ethernet cable. You can buy the original WiPi dongle [here.] (https://www.raspberrypi.org/products/usb-wifi-dongle/)

If you want to buy another, cheaper dongle, [here is the list of working dongles.] (http://elinux.org/RPi_USB_Wi-Fi_Adapters/)

##### 5. Formatting the SD-card
Before you can put any OS on your SD-card, you have to format it first. 

- Download SD formatter [here.] (https://www.sdcard.org/downloads/formatter_4/)
- When you have SD formatter installed, insert the SD card into your computers' card slot
- Make sure that you select the format option "Overwrite format"
- Click the format button and wait. It can take some time, depending on your SD card.

##### 6. Download OS for the Pi
After the SD card is done formatting, you have do download Raspbian OS for your Pi. You can download the latest version [here.] (https://www.raspberrypi.org/downloads/)
- If you are new to this, download the NOOBS OS, as it is the most user-friendly. 
- After the OS has downloaded, unzip the file, and copy the whole content of the folder over to your SD-card.

Your SD card is now ready to be inserted to your Raspberry Pi!

You'll also need to install Node (v4.0.0+) which now comes bundled with npm.
```
wget https://nodejs.org/dist/v4.0.0/node-v4.0.0-linux-armv7l.tar.gz 
tar -xvf node-v4.0.0-linux-armv7l.tar.gz 
cd node-v4.0.0-linux-armv7l
```
Copy to /usr/local
```
sudo cp -R * /usr/local/
```

##### Getting the code
Next up you'll want to clone this repository into your user's home folder on your Pi:
```
cd ~
git clone https://github.com/evancohen/smart-mirror.git
```

##### Configuring the mirror
You'll need to fill in two things into `js/config.js`:

1. A [Forecast API key](https://developer.forecast.io/) (don't worry it's free)
2. Philips Hue Bridge IP address with a configured user. Details about how to set this up in the [Philips Hue Developer Documentation](http://www.developers.meethue.com/documentation/getting-started)
3. [Optional] An array of iCal addresses (from your Google or Outlook calendar for example)

The format of your config should look something like this:
```
var FORCAST_API_KEY = "a6s5dg39j78qj38sjs91je9djadfa1e";
var HUE_BASE = "http://192.168.1.99/api/as9234ho0dfhoq01f2as3yh4m0/";
var PERSONAL_CALENDAR = ["https://calendar.google.com/calendar/ical/SOMESTUFF/basic.ics",
"https://outlook.office365.com/owa/calendar/SOMESTUFF/reachcalendar.ics"];
```
##### Configuring the Pi
In order to rotate your monitor you'll need to add the following line to `/boot/config.txt`
```
display_rotate=1
```
You can also set this value to '3' to have a flipped vertical orientation.

In order to disable the screensaver you'll want to comment out (with a '#') the `@xscreensaver` and `@lxpanel` lines in `/etc/xdg/lxsession/LXDE/autostart`. You'll also want to add the following lines to that same file
```
@xset s off
@xset -dpms
@xset s noblank
```

##### Install dependencies and run
Before we can run the thing we've got to install the projects dependencies. From the root of the `smart-mirror` directory run:
```
npm install
```

This will take a minute, it has to download [electron-prebuilt](https://github.com/mafintosh/electron-prebuilt). Once that is done you can launch the mirror with
```
npm start
```

#### Development
To launch the mirror with a debug window attached use the following command:
```
npm start dev
```
More info coming soon(ish). In the meantime head over to the [gitter chat](https://gitter.im/evancohen/smart-mirror) for help. 

#### Troubleshooting
If you are having trouble getting a USB microphone to work on your Pi try following [these steps](https://github.com/evancohen/smart-mirror/issues/20)

### License
MIT

### Author
[Evan Cohen](http://evanbtcohen.com/)

### More info
Favicon from [In the Wake of the King](http://walkingmind.evilhat.com/2014/03/17/in-the-wake-of-the-king/), a head nod to **The Watcher** – "A byblow of the king and a queen of the sea, she has remained apart from the workings of her family, more home beneath the waves, watching all through water and mirror. Her ambitions lie outside the Eternal Kingdom, but her secrets are valuable everywhere."

Awesome.
