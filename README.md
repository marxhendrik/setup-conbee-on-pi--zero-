# setup conbee 2 on pi (zero)
because it took a lot of time to figure out I keep it here

## Tech
Raspberry Pi Zero with Raspbian
Conbee2 Zigbee dongle
USB->Mini USB Adapter (with OTG?)

## Power
First Pi did not work. Another USB cable Power Adapter worked. I am using a USB->Mini adapter with OTG (not sure if that is needed). The original power supply supplied only 0.2A

## Install deConz
Install deConz like is described on https://phoscon.de/en/conbee/

## Desktop UI
Even if you are running the pi without Monitor you need to have the Desktop enabled :( 

`$ raspi-config` 

In the same screen you can enable VNC if you want it (I ended up not needing it)

## Port
run service with 

`sudo systemctl enable deconz` 

It will run on part 80. For me it did not work. Change the port with

`sudo systemctl edit deconz` 

And add this

```
User=pi
# /etc/systemd/system/deconz.service.d/override.conf
[Service]
ExecStart=
ExecStart=/usr/bin/deCONZ -platform minimal --http-port=8080 --ws-port=8081 --auto-connect=1 --dbg-error=1
```
I am not sure the first line (pi is the user) is necessary but I copied it from somewhere and I am not going to do experiments now that it works ;D

## Logging In
Now you should be able to go to http://IP:8080/pwa/login.html
