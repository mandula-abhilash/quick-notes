sudo apt-get update

sudo apt-get upgrade

sudo ufw allow 8080

sudo ufw status

sudo apt-get install gdal-bin
gdalinfo --version


apt-get install software-properties-common

## Add mirror with openjdk-8-jdk

apt-add-repository 'deb http://security.debian.org/debian-security stretch/updates main'
apt-get update

## Install openjdk 8

apt-get install openjdk-8-jdk

sudo ln -s /usr/lib/jvm/java-8-openjdk-amd64/jre/ /usr/lib/jvm/jre

Set default Java version: https://computingforgeeks.com/how-to-set-default-java-version-on-ubuntu-debian/

sudo update-alternatives --config java
sudo  update-alternatives --config javac

java -version

## GeoServer Installation

- Navigate to the [GeoServer Download page](http://geoserver.org/download/)
- Select the version of GeoServer that you wish to download. If you’re not sure, select Stable release.
- Select Platform Independent Binary on the download page

```
sudo apt-get update
sudo apt-get install zip unzip

sudo mkdir /usr/share/geoserver
cd /usr/share/geoserver
sudo wget --no-check-certificate https://sourceforge.net/projects/geoserver/files/GeoServer/2.20.4/geoserver-2.20.4-bin.zip
sudo unzip geoserver-2.20.4-bin.zip
sudo rm -rf geoserver-2.20.4-bin.zip

echo "export GEOSERVER_HOME=/usr/share/geoserver" >> ~/.profile
. ~/.profile
sudo chown -R abhilash /usr/share/geoserver/

cd /etc/init.d/
sudo wget --no-check-certificate https://docs.geoserver.org/latest/en/user/_downloads/5c56ec58bc153d3a7dd6ef198f9eeaf7/geoserver_deb

sudo mv geoserver_deb geoserver
sudo chmod +x /etc/init.d/geoserver

```

Update values accordingly

```
GEOSERVER_DATA_DIR=/usr/share/geoserver/data_dir
GEOSERVER_HOME=/usr/share/geoserver

PATH=/usr/sbin:/usr/bin:/sbin:/bin
DESC="GeoServer daemon"
NAME=geoserver
JAVA_HOME=/usr/lib/jvm/jre
JAVA_OPTS="-Xms128m -Xmx512m"
PIDFILE=/var/run/$NAME.pid
SCRIPTNAME=/etc/init.d/$NAME

```

Start, stop reload commands

```
sudo systemctl daemon-reload 
sudo systemctl start geoserver
sudo systemctl status geoserver
sudo systemctl stop geoserver
```

Add location to the nginx

```
vi /etc/nginx/sites-available/default

location /geoserver {
     proxy_pass http://localhost:8080;
     proxy_http_version 1.1;           
     proxy_set_header Upgrade $http_upgrade;           
     proxy_set_header Connection 'upgrade';           
     proxy_set_header Host $host;           
     proxy_cache_bypass $http_upgrade;           
     proxy_hide_header X-Powered-By;           
}
```

```
sudo nginx -t
sudo systemctl restart nginx
```
