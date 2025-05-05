# rasp-install-materials
Installation support files for setting up a Pi for OSD.

These scripts are pulled when a new SD card is created for use as an On Screen Display for Occupancy.

## Install a new Raspberry Pi OSD

**<em>This entire process will take over 20 minutes to complete, patience is key.</em>**

Raspberry Pi operating system is installed onto an SD card, the SD card used is important to ensure the Pi runs at optimal speed, 
the card of choice is a SanDisk Ultra microSDHC UHS-I card an Amazon link can be found [here](https://www.amazon.co.uk/dp/B08GY9NYRM?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1). 

* Unpack and insert the SD card into the computer you will use to create the OS (NOT the Pi)
* Download a copy of Raspberry Pi Imager [here](https://www.raspberrypi.com/software/)
* Follow the video below (make sure the audio is switched on) to select the appropriate operating system and WiFi configuration

[video link](https://github.com/sanicus-iot/rasp-install-materials/raw/refs/heads/master/setup-pi.mp4)

Once the SD card is written and ejected:

**ENSURE THE Pi IS POWERED OFF**

Insert the SD card into the Pi (small SD cardholder on the bottom of the Pi )

![SD Install Location](https://github.com/sanicus-iot/rasp-install-materials/raw/refs/heads/master/pi-card.png "SD Install")

Now plug the WiFi aerial into one of the blue USB ports on the rear of the Pi

![Aerial](https://github.com/sanicus-iot/rasp-install-materials/raw/refs/heads/master/Aerial.png "Aerial")

Power the Pi on.

After about 2 minutes you can SSH onto the Pi to continue the installation.

Open a terminal (Putty on windows) and type the following:

```console
ssh pi@occupancy.local
```
You may be presented with the following warning:
![Warning](https://github.com/sanicus-iot/rasp-install-materials/raw/refs/heads/master/ssh-warning.png "Warning")
If you are, just type **yes** followed by enter.

You will be prompted for the password entered (this is the Pi password provided when creating the Pi OS)

```console
wget "https://github.com/sanicus-iot/rasp-install-materials/raw/refs/heads/master/download-materials"
bash download-materials
```
This will start the first phase of the installation - the Wifi card - once complete the Pi will reboot - this is perfectly normal.

Once the Pi has restarted you should see a green flashing light on the Aerial.

Connect again 

```console
ssh pi@occupancy.local
bash pi-install.sh
```
At the end of this process the system will open 'raspi-config' 

![Raspi Config](https://github.com/sanicus-iot/rasp-install-materials/raw/refs/heads/master/raspi-config.png "Raspi Config")

Select '**System Options**', followed by '**S5 Boot/Auto Login**', followed by '**B2 Console Auto Login**'.
The console may go blank for a short time, once it is visible again move the cursor (with the arrow keys) to the bottom then press the right arrow twice and select finish.

The question 'would you like to reboot', select 'yes'... the system will reboot.

### Setting the occupancy washroom and Designation

```console
ssh pi@occupancy.local
bash ./set-occupancy
```
You will be asked to enter the 

This will complete the software installation
