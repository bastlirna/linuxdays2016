# Workshop Dratujeme IoT :: Node-RED



## Úvod

## 1. Instalace

### Instalace node.js

Instalace **node.js** (min 0.10.x, lepší 4.x, ale zas ne 5.x *;)* )

	sudo apt-get install nodejs

Instalace **npm** (node package manager).

	sudo apt-get install npm

Ubuntu instaluje node.js jako `nodejs`, ale Node-RED očekává `node`

	sudo ln -s "$(which nodejs)" /usr/bin/node

### Instalace Node-RED

Použijeme npm (*-g* znamená globání balíček, *--unsafe-perm* )

	sudo npm install -g --unsafe-perm node-red

*Poznámka:* Pro instalaci na PROD prostředí prostudujte [dokumentaci](http://nodered.org/docs/getting-started/installation).


## 2. Konfigurace a spuštění

### První spuštění

	node-red

Otevřít v prohlížeči **[http://localhost:1880](http://localhost:1880)**

### Konfigurace

Při prvním spuštění se vytvoří adresář v *homu*

	cd ~/.node-red/

V něm je

-  `settings.js` — nastavení parametrů, zabezpečení, https,... 
-  `*.json` — uložená flow
-  `node_modules` — node.js moduly (pluginy pro Node-RED)

## 3. První FLOW

- Vytvořit flow (inject, debug)
- Deploy

## 4. Druhé FLOW

- JS node

### Kam dál

- [http://flows.nodered.org/](http://flows.nodered.org/)

## 5. Instalace nodes

### UI Contrib

	cd ~\.node-red
	npm install node-red-contrib-ui

**Pozor:** bez `sudo` a bez `-g` (instalace jen do adresáře `.node-red`)

URL: **[http://localhost:1880/ui](http://localhost:1880/ui)**


## Odkazy

- [http://nodered.org](http://nodered.org)
- [http://flows.nodered.org/](http://flows.nodered.org/)
- [http://noderedguide.com/](http://noderedguide.com/)
- [https://www.youtube.com/watch?v=ZO8wCqcCKGE](https://www.youtube.com/watch?v=ZO8wCqcCKGE) - přednáška v rámci SUT ([slidy](http://www.slideshare.net/ah01/nodered-55231642))

