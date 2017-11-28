# What is this?

I wanted to do some testing with Zabbix locally so created this repository from the zabbix-docker repository, stripped it down, modified some settings, and added some simple instructions to get Zabbix up and going quickly.

This is based off the zabbix-docker apline mysql 3.4.4 release: https://github.com/zabbix/zabbix-docker/releases/tag/3.4.4

This is NOT intended to be used other than anything but local testing purposes.

I have no affiliation with Zabbix.

# What is Zabbix?

Zabbix is an enterprise-class open source distributed monitoring solution.

Zabbix is software that monitors numerous parameters of a network and the health and integrity of servers. Zabbix uses a flexible notification mechanism that allows users to configure e-mail based alerts for virtually any event. This allows a fast reaction to server problems. Zabbix offers excellent reporting and data visualisation features based on the stored data. This makes Zabbix ideal for capacity planning.

For more information and related downloads for Zabbix components, please visit https://hub.docker.com/u/zabbix/ and https://zabbix.com

### Base Docker Image

* [alpine](https://hub.docker.com/_/alpine/)

### Setup

1. Fire up those containers:
```
docker-compose up
```

2. Go to the Zabbix web interface: [Zabbix web interface](http://localhost/) username: Admin password: zabbix

3. Create a host. From the web interface, go to Configuration->Hosts and "Create Host" with the following settings:

    Host:
    
        * Host name: local
        * Groups->In groups: Zabbix servers
        * Agent interfaces->Ip address: (leave blank)
        * Agent interfaces->DNS name: zabbix-agent
        * Agent interfaces->Connect to: DNS
        * Agent interfaces->Port: 10050
    
    Templates:
    
        * Template App Zabbix Server
        * Template OS Linux
    
    IPMI:
    
        * Authentication algorithm->Default
        * Privilege level->User
    
    Encryption:
    
        * Connections to host: No encryption
        * Connections from host: No encryption

4. Create a proxy. From the web interface, go to Administration->Proxies and "Create Proxy" with the following settings:

    Proxy:

        * Proxy name: zabbix-proxy-mysql
        * Proxy mode: Active
        * Hosts->Proxy hosts: local

    Encryption:

        * Connections to proxy: No encryption
        * Connections from proxy: No encryption

4. Check out some graphs! From the web interface, go to Monitoring->Graphs

### Usage

Please follow usage instructions of each component image:

Zabbix components:

* [zabbix-agent](https://hub.docker.com/r/zabbix/zabbix-agent/) - Zabbix agent
* [zabbix-server-mysql](https://hub.docker.com/r/zabbix/zabbix-server-mysql/) - Zabbix server with MySQL database support
* [zabbix-web-apache-mysql](https://hub.docker.com/r/zabbix/zabbix-web-apache-mysql/) - Zabbix web interface on Apache2 web server with MySQL database support
* [zabbix-proxy-mysql](https://hub.docker.com/r/zabbix/zabbix-proxy-mysql/) - Zabbix proxy with MySQL database support
* [zabbix-java-gateway](https://hub.docker.com/r/zabbix/zabbix-java-gateway/) - Zabbix Java Gateway
* [zabbix-snmptraps](https://hub.docker.com/r/zabbix/zabbix-snmptraps/) - Additional container image for Zabbix server and Zabbix proxy to support SNMP traps

Other components:
* [phpmyadmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/) - A web interface for MySQL and MariaDB
