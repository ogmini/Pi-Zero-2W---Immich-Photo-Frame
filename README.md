# Pi Zero 2W ImmichPhoto Frame
I wanted a digital photo frame that I could give to my parents so they could see photos of my family. I had the following requirements:

- No cloud service/subscription
  - [Immich](https://immich.app/) 
- Minimal setup for my parents (Plug and Play)
  - Ability to troubleshoot remotely 
- Secure

During my research, I found a great writeup at [https://fanyangmeng.blog/build-a-selfhosted-digital-frame/](https://fanyangmeng.blog/build-a-selfhosted-digital-frame/) which was almost exactly what I was looking for. I made some changes and I'll be documenting my setup below. I highly encourage reading his writeup.

## Hardware
- Raspberry Pi Zero 2 W
- SpotPear Pi Zero 2W 7inch LCD DIY Tablet Touch Screen Display [https://www.aliexpress.us/item/3256804812995753.html](https://www.aliexpress.us/item/3256804812995753.html)
- MicroSD Card
- Heatsink [https://www.amazon.com/Geekworm-Raspberry-Heatsink-Aluminumn-Compatible/dp/B09QMBCXLB](https://www.amazon.com/Geekworm-Raspberry-Heatsink-Aluminumn-Compatible/dp/B09QMBCXLB)

Installing the heatsink required some "modifications" to the PCB for the MicroSD Card. I had to use a dremel and clearance the board by cutting off the screwhole ears. Additionally, the screws that came with the heatsink were a tad too long and had to be spaced out a bit. I used some DIY thin cardboard "washers" to accomplish this spacing. You could also possibly sand down the screws.

## Software
- DietPi [https://dietpi.com/](https://dietpi.com/)
- Tailscale [https://tailscale.com/](https://tailscale.com/)
- Immich [https://immich.app/](https://immich.app/) 
- Immich Kiosk [https://github.com/damongolding/immich-kiosk](https://github.com/damongolding/immich-kiosk)

### Immich
Have this setup already...

Create an album to contain any photos that you want to be used by Immich Kiosk. This album can be shared so that other people can add photos. You will also need to create an API Key for Immich Frame. For my purposes I gave it the following permissions:
- asset.read
- asset.view
- album.read
- album.statistics
- archive.read
- face.read
- memory.read
- person.read
- person.statistics
- server.about
- tag.read
- user.read
 
More details about the API Permissions needed can be found at [https://docs.immichkiosk.app/installation/#api-key-permissions](https://docs.immichkiosk.app/installation/#api-key-permissions)

I can probably remove some of these permissions.

### Immich Kiosk
I followed the docker installation instructions found at [https://docs.immichkiosk.app/installation/#docker-recommended](https://docs.immichkiosk.app/installation/#docker-recommended) doing Option 1 and adding to my existing compose stack.

### DietPi
I followed the installation instrructions from DietPi with the following changes to the config.txt file in the install files.

```
hdmi_force_hotplug=1 
config_hdmi_boost=10
hdmi_group=2 
hdmi_mode=87 
hdmi_cvt 1024 600 60 6 0 0 0
```

Using dietpi-software, I installd the following:
- LXDE
- OpenSSH
- Chromium

I installed Tailscale seperately

```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```

#### Configuration File Changes

##### /boot/dietpi.txt
I would encourage you to read this over and make appropriate changes. I changed the following:
```
SOFTWARE_CHROMIUM_RES_X=1024
SOFTWARE_CHROMIUM_RES_Y=600
```
##### Chromium Autostart

##### CRON Jobs



