# Capstone
this is a repository for my Capstone Project


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


