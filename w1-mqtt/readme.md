Drátujeme IoT :: MQTT
============
*MQTT* - Message Queuing Telemetry Transport je malý a jednoduchý protokol pro komunikaci senzorů a mobilních zařízení. Pracuje na principu publish/subscribe jednoduchých textových zpráv.

Další informace http://www.hivemq.com/blog/mqtt-essentials/

Podporuje 
* QoS
    0. Maximálně jednou (At most once)
    1. Minimálně jednou (At least once) 
    2. Přesně jednou (Exactly once)
* Retain - ukládat zprávu na serveru
* Last Will and Testament
* Wildcard
    * Singlelevel 
    * Multilevel

## Obsah workshopu
1. MQTT Spy
2. Instalace
3. Přístupová práva
4. Websockets
5. Log do MQTT kanálu

## 1. MQTT Spy
**MQTT Spy** je pub/sub client pro *MQTT* prtokol.
Pro instalaci a spuštění pod uživatelem *linuxdays* spuste tyto příkazy

    sudo apt-get install openjdk-8-jre openjfx
    wget https://github.com/kamilfb/mqtt-spy/releases/download/mqtt-spy_v0.5.4/mqtt-spy-0.5.4-jar-with-dependencies.jar
    java -jar mqtt-spy-0.5.4-jar-with-dependencies.jar
## 2. Instalace
### Instalace MQTT brokeru
    sudo apt-get install mosquitto mosquitto-clients
## 3. Přístupová práva
Následující příkazy vyžadují oprávnění uživatele *root*

    cd /etc/mosquitto/
    touch conf.d/acl.conf
    touch mosquitto.acl
    
Do souboru **conf.d/acl.conf** přidat
    
    acl_file /etc/mosquitto/mosquitto.acl
    password_file /etc/mosquitto/mosquitto.passwd
    allow_anonymous true
 
 Do souboru **mosquitto.acl** přidat   
    
    topic read #
    topic readwrite /tmp/#
    topic read $SYS/#
    
    user john
    topic readwrite #
    
Založíme uživatele **john** s heslem **doe** a upravíme práva k souboru s hesly

    mosquitto_passwd -c mosquitto.passwd john
    chmod o-r mosquitto.passwd 
Restartujeme **mosquitto**
    
    systemctl restart mosquitto.service
Pro zkoušku ACL můžeme využít tyto příkazy

    mosquitto_pub -h localhost -t /test -m "test data" -u john -P doe
    mosquitto_pub -h localhost -t /test -m "test data"
    mosquitto_pub -h localhost -t /tmp/tst -m "test data"
    mosquitto_sub -h localhost -t /#
## 4. Websockets   
Vytvoříme konfiguraci pro protokol *mqtt*

    touch conf.d/mqtt.conf
V souboru **conf.d/mqtt.conf**
    
    listener 1883 127.0.0.1
    protocol mqtt
    
Vytvoříme konfiguraci pro *websocket*

    touch conf.d/websocket.conf
V souboru **conf.d/websocket.conf**

    listener 9001 127.0.0.1
    protocol websockets
    http_dir /var/www
Vytvoříme adresář s MQTT Wall

    mkdir /var/www
    chown mosquitto:mosquitto /var/www
    cd /var/www
    wget https://github.com/bastlirna/mqtt-wall/releases/download/v0.2/mqtt-wall-0.2.0.zip
    unzip mqtt-wall-0.2.0.zip
    mv wall-0.2.0/* .
    rm wall-0.2.0/ -r
    rm mqtt-wall-0.2.0.zip
Upravit v **/var/www/index.html** adresu serveru pro připojení na
    
    localhost:9001
A poté restartovat mosquitto
    
    systemctl restart mosquitto.service
Nyní na adrese **http://localhost:9001** je dostupná stránka s MQTT Wall

## 5. Log do MQTT kanálu **$SYS/broker/log/#**
Vytvoříme konfiguraci pro log

    touch conf.d/logging.conf
S obsahem
    
    log_dest topic
