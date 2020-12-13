# Export des alten fablab Wiki

Ich habe folgendes Tool verwendet:
https://github.com/outofcontrol/mediawiki-to-gfm

Zuerst muss man der Anleitung folgen, [wie man die Seiten des MediaWiki exportiert](https://github.com/outofcontrol/mediawiki-to-gfm).

Danach habe ich folgendes installiert und ausgeführt: 

```
sudo apt update
sudo apt install php
sudo apt install php7.4-xml
sudo apt install pandoc
sudo apt install composer
sudo apt install git
git clone https://github.com/outofcontrol/mediawiki-to-gfm.git
cd mediawiki-to-gfm
composer update --no-dev
cd ..
../mediawiki-to-gfm/convert.php --filename=./fablab+Cottbus-20201213193957.xml 
```

Danach hatte ich einen Ordner "output" mit allen Seiten im Github Markdown Format. 

Zusätzlich habe ich noch alle Bilder über ftp runter geladen und in den gleichen Ordner gepackt. Diese befanden sich im Ornder `/wiki/mediawiki/images`. Mit folgendem Befehl habe ich die Bilder aus den einzelnen Unterordnern in einem gemeinsamen Ordner gesammelt:

```
mv images/* all_images/
```
