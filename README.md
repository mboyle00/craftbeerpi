# CraftBeerPI v0.1
                                                         
## Features

* Temperaturverlaufsanzeige (Real-Time)
* Frei Konfigurierbarer Ablaufplan mit manuellen und automatischen Schritten
* Timer mit automatischem Start bei erreichen der Zieltemperatur
* Digitales Brauprotokoll
* Smartphone und Tablet optimiert 
* WebSocket Push Notification für Real-Time Update
* Admin Oberfläche
* WLAN Zugriff
* Automatische Heizsteuerung (PID Controller)
* Sud Import aus dem "kleinen Brauhelfer"

## Screenshots

![ScreenShot](https://raw.githubusercontent.com/Manuel83/craftbeerpi/master/docs/images/Screenshot1.png)
![ScreenShot](https://raw.githubusercontent.com/Manuel83/craftbeerpi/master/docs/images/Screenshot2.png)


## Installation

### Raspbian installieren (Noobs)

Hier findet ihr eine Anleitung zur Installation von Noobs.

https://www.raspberrypi.org/help/noobs-setup/

Bitte als Betriebsystem Raspbian auswählen.

### WIFI Auf dem Raspberry PI konfigurieren

Nach WLAN scannen
```
sudo iwlist wlan0 scan
```
WLAN Config Datei öffnen
```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
Netzwerk und Passwort eingeben
```
network={
    ssid="The_ESSID_from_earlier"
    psk="Your_wifi_password"
}
```
WLAN Adapter stoppen
```
sudo ifdown wlan0
```
WLAN Adapter starten
```
sudo ifup wlan
```
### WiringPi installieren
```
sudo apt-get update
sudo apt-get upgrade
git clone git://git.drogon.net/wiringPi
cd wiringPi
git pull origin
cd wiringPi
./build
```
### Pip für Python 2.7 installieren
```
sudo apt-get install python-pip
```
### CraftBeer PI herunterladen
Am einfachsten ist wenn man die Software in das Home Verzeichnis des Benutzers pi wie folgt kopiert
```
git clone https://github.com/Manuel83/craftbeerpi.git
```
### Python Pakete Installieren

Ins CraftBeerPI Verzeichnis wechseln und folgenden Befehlt ausführen
```
sudo pip install -r requirements.txt
```
### Konfiguration

Die Konfiguraitonsdatei ist in folgenen Verzeichnis zu finden

craftbeerpi/brewapp/globalprops.py

```
nano globalprops.py
```


Konfiguraitonsdatei

```
## if test mode
testMode = False

### File name of sonder file
tempSensorId = '28-03146215acff'

### GPIO Number for Heating
heating_pin = 17

## GPIO Number Agitator
agitator_pin = 18

## interval in which the new temperatur is read
temp_db_interval = 5

## heating interval in seconds
pid_interval = 5

## PID tuning parameter
pipP=102

pidI=100

pidD=5

## hysteresis parameter in degrees celsius
## For exmpale. If current temperatur is more than 2 degrees below the traget temp turn the heating 100% on
hysteresis_min=2
## For exmpale. If current temperatur is more than 0.5 degrees higher the traget temp turn the heating 100% off
hysteresis_max=0.5


###################################################################
#### INTERNAL DO NOT CHANGE PARAMETERS BELOW
gpioMode = False
heatingState = False
agitatorState = False
pidState = False
```


### Start der Anwendung

In das carfbeerpi verzeichnis wechseln 
```
sudo nohub python runserver.py &
```

```

   _____            __ _   ____                 _____ _____ 	_.._..,_,_	
  / ____|          / _| | |  _ \               |  __ \_   _|   (          )	
 | |     _ __ __ _| |_| |_| |_) | ___  ___ _ __| |__) || |      ]~,"-.-~~[	
 | |    | '__/ _` |  _| __|  _ < / _ \/ _ \ '__|  ___/ | |    .=])' (;  ([			
 | |____| | | (_| | | | |_| |_) |  __/  __/ |  | |    _| |_   | ]:: '    [			
  \_____|_|  \__,_|_|  \__|____/ \___|\___|_|  |_|   |_____|  '=]): .)  ([		
                                                                |:: '    |
 ---------------------------------------- (C) 2015 Manuel F.     ~~----~~

SET GPIO AGITATOR
AGITATOR GPIO ERROR
SET GPIO HEATING
HEATING GPIO ERROR
START PID
 START TEMP JOB
START STEP JOB
 * Running on http://0.0.0.0:5000/
```


## Hardware Setup für den Testaufbau

* 1 x 1-wire Temperatursensor DS1820
* 1 x 4.7k Ohm Widerstand
* Jumper Kabel (ebay) (Am besten gleich alle Varianten kaufen Stecker-Buchse, Buchse-Buchse, Stecker-Stecker So hat man Spielraum)
* 2 x Solid-State Relais XURUI
* Strangkühlkörper KAB-60
* Labor-Steckboard SYB-46
* Raspberry Pi (Model A+, 2 Model B) + Netzkabel + passende SDCard
* 2 x Steckdose
* Schrauben zum befestingen der Bauteile


![ScreenShot](https://raw.githubusercontent.com/Manuel83/craftbeerpi/master/docs/images/Hardwaresetup.png)
![ScreenShot](https://raw.githubusercontent.com/Manuel83/craftbeerpi/master/docs/images/Hardwaresetup2.png)