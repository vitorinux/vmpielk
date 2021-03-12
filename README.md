# WORK IN PROGRESS... 
try at your own!

## vmpielk
ELK 7.11.1 SUITE for Raspberry pi 4 (4GB arm64) with beats *(auditbeat, filebeat, heartbeat, metricbeat and packetbeat)*

### Results of Metricbeat RPi4 4GB (ELK suite + beats)

![VMELK](https://user-images.githubusercontent.com/24867437/110994917-d3a4b380-8379-11eb-99a7-14688e310d12.png)


## OS Requirements
- RPI 4 4GB (8GB recommended)
- Raspbian or Ubuntu arm64 OS based (aarch64)
- 64GB of Storage (boot from SSD recommended)
- Clone FORK easyBEATS from vitorinux to compile BEATS (only for arm64 OS)
	- https://github.com/vitorinux/easyBEATS.git
- 2 cups of coffee




### Install preconfigured Elasticsearch, Kibana and Logstash *(not required but let's try)* 

Go to web link and download the following arm64 DEB files *(select 7.11.1 release from https://www.elastic.co/downloads/)*
 - elasticsearch-7.11.1-arm64.deb
 - kibana-7.11.1-arm64.deb
 - logstash-7.11.1-arm64.deb

### ELK RAM Requirements (configure jvm.options file)
- Elasticsearch (-Xms1g and -Xmx1g)
- Logstash 600mb (-Xms600m and -Xmx600m)
- Kibana (default)


### In order to boot rpi and not take long time, there are SYSTEMD unit files to delay boot of kibana and logstash
Modify Kibana.service to start after elasticseearch.service

kibana.service 
```
[Unit]
Description=Kibana
Documentation=https://www.elastic.co
Wants=network-online.target
After=network-online.target elasticsearch.service
...
... lines removed ...
...

```

Create a file .timer on the path of your .service file (wait 300s before start the process)

kibana.timer 
```
[Unit]
Description=Start KIBANA after 300s

[Timer]
OnBootSec=300s

[Install]
WantedBy=timers.target

```

Do the same for Logstash

logstash.service

```
[Unit]
Description=logstash
Wants=network-online.target
After=network-online.target elasticsearch.service
...
... lines removed ...
...
```

logstash.timer
```
[Unit]
Description=Start LOGSTASH after 300s

[Timer]
OnBootSec=300s

[Install]
WantedBy=timers.target

```



### Install BEATS arm64 with easyBEATS
Follow instructions...









