# Capstone
this is a repository for my Capstone Project


# Update system
sudo apt update -y && sudo apt upgrade -y

# Install required packages for Raspberry Pi 3+ (either a or B as long as its a 3)
sudo apt --no-install-recommends install python3-pip libcamera-v4l2 libcamera-tools python3-dev libcurl4-openssl-dev libssl-dev -y

# Install MotionEye
sudo python3 -m pip install --pre motioneye --break-system-packages

# Initialize MotionEye
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
