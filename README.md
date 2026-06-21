# DomainTools
RaspberryPi DomainTools


#Update RaspberryPi
sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y

#Install rpi-connect-ota package
sudo apt install rpi-connect-ota -y

#Keep Systemd Manager Running Even After Log Out
loginctl enable-linger

#Configure Static Networks
sudo nmtui

#Install Needed Packages
sudo apt install dnsmasq -y

#Make a backup of the config file
cp /etc/dnsmasq.conf ~/dnsmasq.conf.backup

# Crontab entries
sudo crontab -e
0 0 * * * apt update && apt dist-upgrade -y && apt autoremove -y && apt-get clean && apt-get autoclean
0 5 * * * reboot --force

#Disable WiFi Power Management
sudo nano /etc/systemd/system/wifi-powermanagement-off.service
[Unit]
Description=Disable WiFi Power Management
After=network.target

[Service]
Type=oneshot
ExecStart=/sbin/iwconfig wlan0 power off
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

sudo systemctl enable wifi-powermanagement-off
sudo systemctl start wifi-powermanagement-off


#Disable WiFi Power Save
sudo nano /etc/systemd/system/wifi-powersave-off.service
[Unit]
Description=Disable WiFi Power Save
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/sbin/iw dev wlan0 set power_save off
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload
sudo systemctl enable wifi-powersave-off.service
sudo systemctl start wifi-powersave-off.service
