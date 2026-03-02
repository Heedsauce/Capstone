# Capstone
this is a repository for my Capstone Project

# Parts
Raspberry Pi Camera Module 3

https://www.amazon.com/Raspberry-Pi-Camera-Module/dp/B0BRY6MVXL

Raspberry Pi 3 A+ (you can use a better version I chose this to keep the cost down) 

https://www.amazon.com/Raspberry-Pi-3-Computer-Board/dp/B07KKBCXLY/ref=sr_1_1?sr=8-1

Raspberry Pi 3 Case: Camera Mount, USB & Network Access 

https://www.etsy.com/listing/1864540495/raspberry-pi-3-case-camera-mount-usb?ref=yr_purchases

Raspberry Pi 3 / Zero Power Supply (Micro USB) This is the cord that I have for testing purposes your welcome to get another as long as it has 3.5v of power

https://www.canakit.com/raspberry-pi-3-zero-power-supply-micro-usb.html

SD Card Reader

https://www.amazon.com/acer-Adapter-MicroSD-Compatible-iPhone16/dp/B0DQ71G4G4/ref=sr_1_2_sspa?sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY

SD Cards that have the Micro SD IN them

https://www.amazon.com/Lexar-Micro-microSDHC-Memory-Adapter/dp/B09JNL9VSR/ref=sxin_28_pa_sp_search_thematic_sspa?cv_ct_cx=micro%2Bsd%2Bcard&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sr=1-1-7efdef4d-9875-47e1-927f-8c2c1c47ed49-spons&aref=6Ex20MlsvY&sp_csd=d2lkZ2V0TmFtZT1zcF9zZWFyY2hfdGhlbWF0aWM

These should be all the parts you need for the Camera
# Starting the Pi
BEFORE you plug in the raspberry Pi go to this website https://www.raspberrypi.com/software/ and download the Raspberry Pi imager. 
This allows you to put the desiered OS onto the raspberry Pi
Run the Program and Plug in the SD to USB card reader and follow the instructions on screen
Enable SSH and remember the usernamename and hostname you gave it as it is important in the next step

# First Login
After you put the SD card into the Raspbery Pi connect it to whatever powercord/source you have and WAIT until the GREEN light stops blinking.
The Green light means it is reading from the card and starting to boot
After the green light is solid then go to your command line and type in  ssh@USERNAME@HOSTNAME.local and you should see a screen asking for a fingerprint, say yes
After you say Yes you will be connected to the Pi!
# Update system
sudo apt update -y && sudo apt upgrade -y

# Install required packages for Raspberry Pi 3+ (either a or B as long as its a 3)
sudo apt --no-install-recommends install python3-pip libcamera-v4l2 libcamera-tools python3-dev libcurl4-openssl-dev libssl-dev -y

# Install MotionEye
sudo python3 -m pip install --pre motioneye --break-system-packages

The reason you have to do the --break-system-packages is because this is only supposed to run in Virtual Machines but because of the technology restraint we have using the Pi 3 we are using the whole Pi to run it 

# Initialize MotionEyee usi
sudo motioneye_init

# Add libcamerify compatibility layer
sudo sed -i 's|ExecStart=/usr/local/bin/meyectl startserver -c /etc/motioneye/motioneye.conf|ExecStart=/usr/bin/libcamerify /usr/local/bin/meyectl startserver -c /etc/motioneye/motioneye.conf|' /etc/systemd/system/motioneye.service
# OR
sudo nano /etc/systemd/system/motioneye.service
Find this line: ExecStart=/usr/local/bin/meyectl startserver -c /etc/motioneye/motioneye.conf

Change it to this:
ExecStart=/usr/bin/libcamerify /usr/local/bin/meyectl startserver -c /etc/motioneye/motioneye.conf

# Reload and restart service
sudo systemctl daemon-reload
sudo systemctl restart motioneye.service

# Enable on boot (optional)
sudo systemctl enable motioneye.service

To access Motion eye in your browser go to http://[RASPBERRY_PI_IP]:8765
The website will stream videos and also offers a way to customize the camera settings with things like resolution, framerate,rotation and more importantly MOTION DETECTION

# Motioneye Config
after motioneye is installed there should be a very nice and simple dashboard for you to use and play around with 
# or
if you want to use my config file just download the Final-motioneye-config.tar.gz and import it from the GUI 
My config has it running at 30fps and a resolution of 1280 x 1024 which is the maximum for the Pi Camera 3 

# Website 
There is also a website on this page aswell to run locally on your machine.
Download the Zip file and Open it in your favorite coding application 
Open the terminal and type in python proxy.py

