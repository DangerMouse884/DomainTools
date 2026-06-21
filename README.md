# RaspberryPi DomainTools ReadMe

# Update RaspberryPi
sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y

# Install rpi-connect-ota package
sudo apt install rpi-connect-ota -y

# Install Needed Dnsmasq Packages
sudo apt install dnsmasq -y

# Backup Original Dnsmasq Config File
cp /etc/dnsmasq.conf ~/dnsmasq.conf.backup

# Keep Systemd Manager Running Even After Log Out
loginctl enable-linger

# Configure Static Networks - Using NetworkManager Text User Interface
sudo nmtui

# Reload Systemd Manager's Configuration
sudo systemctl daemon-reload

# Enable/Start wifi-powermanagement-off Service
sudo systemctl enable wifi-powermanagement-off.service\
sudo systemctl start wifi-powermanagement-off.service

# Enable/Start wifi-powersave-off Service
sudo systemctl enable wifi-powersave-off.service\
sudo systemctl start wifi-powersave-off.service
