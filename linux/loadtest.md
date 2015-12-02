## JMeter

### JMeter en JMeter plugins installeren (Linux)

Prerequisites:

- Java-versie 6 of hoger

1. Download [JMeter](http://jmeter.apache.org/download_jmeter.cgi): de tarball of zip van de laatste versie en pak uit op de gewenste locatie (bvb /opt/ als je in linux werkt).
2. Download [JMeter Standard Plugins](http://jmeter-plugins.org/downloads/file/JMeterPlugins-Standard-1.3.1.zip) en pak uit in de installatiedirectory van JMeter (bvb. /opt/apache-jmeter-2.13/).
3. Download [deze JRE](https://drive.google.com/file/d/0B9m__Xw-PAR_Y1h0aUhGblFpd0k/view?usp=sharing). Unzip en plaats de map+inhoud in de subfolder jmeter/ServerAgent-2.2.1/ van de stack die je wil testen.


### JMeter opstarten (GUI)

Voer het bash-script 'jmeter' in de bin-directory uit. Voor Windows: jmeter.bat in de bin-directory.
Als je deze directory aan PATH hebt toegevoegd kan dat met `jmeter`, anders moet je het volledige pad naar het script opgeven.


### JMeter testscript uitvoeren

We voeren de testscripts uit in non-GUI mode om zoveel mogelijk factoren weg te nemen die jmeter extra belasten (gui, live graphs)

Navigeer in de cli naar de directory 'jmeter' in de set-up die je wil testen (bvb. lampstack/jmeter). Zo komen de logfiles en de resultaten in deze directory terecht.

`jmeter -n -t TESTBESTAND.jmx`

* Als de directory waar scripts jmeter/jmeter.bat niet in PATH zit, moet je het volledige pad naar dit script opgeven!
* `-n`: jmeter starten in non-GUI mode
* `-t` gevolgd door het testplan dat je wil uitvoeren

Na de test kan je de resultaten bekijken door de GUI te starten, het testplan in te laden, de listener te selecteren en het bestand te laten inladen (knop Browse...).