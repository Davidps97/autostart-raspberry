# Kiosk Setup for Raspberry Pi

This project provides a step-by-step guide to setting up a Raspberry Pi as a kiosk that automatically launches a Chromium browser in kiosk mode. The setup includes creating a systemd service to manage the Chromium browser and configuring LXDE to disable screen saving and power management features.

## Features

- **Automatic Updates**: Ensures your Raspberry Pi is up to date with the latest software.
- **Chromium Browser**: Installs and configures Chromium to run in kiosk mode.
- **Systemd Service**: Creates a service to manage the kiosk application.
- **LXDE Configuration**: Adjusts LXDE settings to prevent screen blanking and power management interruptions.

## Installation

Follow these steps to set up your Raspberry Pi as a kiosk:

### 1. Install Necessary Packages

Update your system and install Chromium and Unclutter.

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y chromium-browser
sudo apt install -y unclutter
```

### 2. Create the Kiosk Service
Create a systemd service to manage the Chromium browser in kiosk mode.

```bash
sudo nano /etc/systemd/system/kiosk.service
```

Add the following code to the service file:

```bash
[Unit]
Description=Chromium Kiosk
After=graphical.target

[Service]
User=definition
Environment=XAUTHORITY=/home/definition/.Xauthority
Environment=DISPLAY=:0
ExecStart=/usr/bin/chromium-browser --noerrdialogs --disable-infobars --kiosk https://your.web.com
Restart=on-abort

[Install]
WantedBy=graphical.target
```

Enable and start the service:

```bash
sudo systemctl enable kiosk.service
sudo systemctl start kiosk.service
```

### 3. Configure LXDE
Adjust LXDE settings to disable screen saving and power management.

```bash
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
```

Add the following lines:

```bash
@xset s off
@xset -dpms
@xset s noblank
@chromium-browser --noerrdialogs --disable-infobars --kiosk https://api.akdeniz-wilhelmshaven.de/?menuCard=lunch
@unclutter -idle 0
```

### Contributing
If you would like to contribute to this project, please submit a pull request or open an issue for any improvements or suggestions.
