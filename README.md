# DomainTools
RaspberryPi DomainTools ReadMe

#Update RaspberryPi
sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y

#Install rpi-connect-ota package
sudo apt install rpi-connect-ota -y

#Install Needed Dnsmasq Packages
sudo apt install dnsmasq -y

#Backup Original Dnsmasq Config File
cp /etc/dnsmasq.conf ~/dnsmasq.conf.backup

#Keep Systemd Manager Running Even After Log Out
loginctl enable-linger

#Configure Static Networks
sudo nmtui

# Add Crontab Entries
sudo crontab -e
0 0 * * * apt update && apt dist-upgrade -y && apt autoremove -y && apt-get clean && apt-get autoclean
0 5 * * * reboot --force

sudo systemctl daemon-reload
sudo systemctl enable wifi-powermanagement-off
sudo systemctl start wifi-powermanagement-off

sudo systemctl daemon-reload
sudo systemctl enable wifi-powersave-off.service
sudo systemctl start wifi-powersave-off.service
