# NGINX Proxy Manager

NGINX Proxy Manager (NPM) is an easy-to-use docker application that gives a simple, powerful web interface for creating and managing Nginx proxy hosts. This application makes configuring reverse proxies a breeze for software stacks that include multiple docker images.

## Installation

This procedure will assume that the user has knowledge of dockSTARTer and how to use the application. For assistance, see the below references.

The official dockSTARTer [documention](https://dockstarter.com/introduction/) is the best place to reference for DS installation and operations support.

The official NGINX Proxy Manager [installation instructions](https://github.com/jc21/nginx-proxy-manager/blob/master/doc/INSTALL.md?utm_source=npm-site) are the best place to reference for understanding the inner workings of how the NPM functions.

### 1) Configure Override

* Navigate to **YOUR-HOME-DIRECTORY**/.docker
* Configure your override as indicated in the below code block. A docker-compose.override.yml is also give in the repository for download or cloning.

    ````yml
    services:
    # NGINX Proxy Manager with LetsEncrypt https://github.com/jc21/nginx-proxy-manager
    proxymanager:
        image: jc21/nginx-proxy-manager:latest
        container_name: proxymanager
        labels:
        - "com.dockstarter.appinfo.description: NGINX Proxy Manager with LetsEncrypt included"
        - "com.dockstarter.appinfo.nicename: NGINX Proxy Manager"
        logging:
        driver: json-file
        options:
            max-file: ${DOCKERLOGGING_MAXFILE}
            max-size: ${DOCKERLOGGING_MAXSIZE}
        ports:
        - "80:80"
        - "81:81"
        - "443:443"
        environment:
        - FORCE_COLOR=1
        - NODE_ENV=config
        volumes:
        - ${DOCKERCONFDIR}/proxymanager/config:/app/config/
        - ${DOCKERCONFDIR}/proxymanager/data:/data
        - ${DOCKERCONFDIR}/proxymanager/letsencrypt:/etc/letsencrypt
        - ${DOCKERSHAREDDIR}:/shared
        depends_on:
        - mariadb
        restart: unless-stopped
    # MariaDB for use with NGINX Proxy Manager https://github.com/MariaDB/server
    mariadb:
        container_name: mariadb
        image: mariadb:latest
        labels:
        - "com.dockstarter.appinfo.description: MariaDB for NGINX Proxy Manager"
        - "com.dockstarter.appinfo.nicename: DB NGINX Proxy Manager"
        logging:
        driver: json-file
        options:
            max-file: ${DOCKERLOGGING_MAXFILE}
            max-size: ${DOCKERLOGGING_MAXSIZE}
        ports:
        - "3306:3306"
        environment:
        - MYSQL_ROOT_PASSWORD=dockstarter
        - MYSQL_DATABASE=proxymgr
        - MYSQL_USER=dockstarter
        - MYSQL_PASSWORD=dockstarter
        - FORCE_COLOR=1
        volumes:
        - ${DOCKERCONFDIR}/mariadb:/var/lib/mysql
        - ${DOCKERSHAREDDIR}:/shared
        restart: unless-stopped

    ````

### 2) Run dockSTARTer

* Run DS from the terminal

    ````bash
    $ ds
    ````

* Navigate to **Configuration > Select Apps**
* Select MariaDB

    ![MariaDB](https://i.imgur.com/v5zc3sm.png)
* Complete DS configuration

### 3) Copy Config File

* Download the config.json file from this repository or clone to the desired location.
* Navigate to **YOUR-HOME-DIRECTORY**/.config/appdata/proxymanager
* Copy the config.json file into this directory

----

This completes the installation. The above process will create two Docker containers:

* proxymanager
* mariadb

Upon successful installation, the MariaDB container will automatically create the database according to the specified environment variables in the **docker-compose.override.xml** file. Once complete, the ProxyManager will be able to communicate with the database with the credientials provided in the **config.json** file. The ProxyManager container requires the mariadb container in order to properly function. It will take a few moments for both to configure and sync up.  

Once complete, both containers will be online with a "healthy" status. The application completion can be validated by a successful navigation to http://localhost:81.
