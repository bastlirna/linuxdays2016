# Drátujeme IoT: Influx DB
Workshop na instalaci a konfiguraci Influx DB a Grafana

## InfluxDB

    mkdir /home/user/influx_grafana
    mkdir /home/user/influx_grafana/install
    cd /home/user/influx_grafana/install
    wget https://dl.influxdata.com/influxdb/releases/influxdb_1.0.2_amd64.deb
    sudo dpkg -i influxdb_1.0.2_amd64.deb
\##
   
    curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
    source /etc/lsb-release
    echo "deb https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
    sudo apt-get update
    sudo apt-get install influxdb
    sudo systemctl start influxdb
    systemctl status influxdb



## Grafana

    cd /home/user/influx_grafana/install
    wget https://grafanarel.s3.amazonaws.com/builds/grafana_3.1.1-1470047149_amd64.deb
    sudo dpkg -i grafana_3.1.1-1470047149_amd64.deb
    curl https://packagecloud.io/gpg.key | sudo apt-key add -
    sudo apt-get update
    sudo apt-get install grafana
    systemctl start grafana-server
    systemctl status grafana-server


## InfluxData

    mkdir /home/user/influx_grafana/data
    cd /home/user/influx_grafana/data
    wget http://iot.siliconhill.cz/wall/ld16/20160718_req_api02.log
    wget http://iot.siliconhill.cz/wall/ld16/20160718_req_db01.log