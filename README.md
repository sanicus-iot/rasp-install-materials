# rasp-install-materials
Installation support files for setting up a Pi for OSD.

These scripts are pulled when a new SD card is created for use as an On Screen Display for Occupancy.

## Install a new Raspberry Pi OSD

**<em>This entire process will take over 20 minutes to complete, patience is key.</em>**

Raspberry Pi operating system is installed onto an SD card, the SD card used is important to ensure the Pi runs at optimal speed, 
the card of choice is a SanDisk Ultra microSDHC UHS-I card an Amazon link can be found [here](https://www.amazon.co.uk/dp/B08GY9NYRM?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1). 
You can also buy the aerial [here](https://www.amazon.co.uk/dp/B07PJV66CN?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1)

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

Type the following two commands on the command line:
```console
wget "https://github.com/sanicus-iot/rasp-install-materials/raw/refs/heads/master/download-materials"
bash download-materials
```
You will be asked for the 'Installation Materials' password

This will start the first phase of the installation - the Wifi card - once complete the Pi will reboot - this is perfectly normal (**This process will take at least 5 minutes**)

Once the Pi has restarted you should see a green flashing light on the Aerial.

Connect again using the command below:

```console
ssh pi@occupancy.local
```
The start the full software install by typing the following command:

```console
bash ./pi-install.sh
```
At the end of this process the system will open 'raspi-config' 

![Raspi Config](https://github.com/sanicus-iot/rasp-install-materials/raw/refs/heads/master/raspi-config.png "Raspi Config")

Select '**System Options**', followed by '**S5 Boot/Auto Login**', followed by '**B2 Console Auto Login**'.
The console may go blank for a short time, once it is visible again move the cursor (with the arrow keys) to the bottom then press the right arrow twice and select finish.

The question 'would you like to reboot', select 'yes'... the system will reboot.

### Setting the occupancy washroom and Designation

Connect to the Pi
```console
ssh pi@occupancy.local
```
Set the occupancy type:
```console
bash ./set-occupancy
```
You will be asked to enter the occupancy ID and the designation

The occupancy ID can be found by using the [Admin Console](https://admin.sanicus-connect.com)

If you select the washroom site on the header, then select assets on the left menu, choose the male/female/prm etc washroom you are interested in and select the 'Info' button on the asset toolbar, you will be presented with a dialog box, 
if you then copy the 'Asset Id' (<em>it will look something like a534044e-c714-4de2-8bee-a281b98434de</em>) and paste this into the occupancy id, then enter a designation MALE/FEMALE etc.

Once you press enter the system will download the latest occupancy screen software and reboot

**NOTE: Once the system reboots it can no longer be accessed as occupancy.local, it will change the host to be <desig>.local e.g. female.local or male.local
