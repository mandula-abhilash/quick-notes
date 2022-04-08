sudo apt-get update

sudo apt-get upgrade

sudo ufw allow 8080

sudo ufw status

sudo apt-add-repository -r ppa:certbot/certbot
sudo apt update
sudo apt-get update

sudo apt-get install gdal-bin
gdalinfo --version

Java Installation steps: https://stackoverflow.com/questions/57031649/how-to-install-openjdk-8-jdk-on-debian-10-buster

Install software source manager

apt-get update
apt-get install software-properties-common

Add mirror with openjdk-8-jdk

apt-add-repository 'deb http://security.debian.org/debian-security stretch/updates main'
apt-get update

Install openjdk 8

apt-get install openjdk-8-jdk

Set default Java version: https://computingforgeeks.com/how-to-set-default-java-version-on-ubuntu-debian/

sudo update-alternatives --config java
sudo  update-alternatives --config javac

java -version

4. GeoServer installation
sudo useradd -m -U -d /opt/tomcat -s /bin/bash tomcat
sudo usermod -a -G www-data tomcat

wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.62/bin/apache-tomcat-9.0.62.tar.gz
sudo tar -xf apache-tomcat-9.0.62.tar.gz -C /opt/tomcat/; rm apache-tomcat-9.0.62.tar.gz

sudo ln -s /opt/tomcat/apache-tomcat-9.0.62 /opt/tomcat/latest

sudo chown -R tomcat:www-data /opt/tomcat/
sudo sh -c 'chmod +x /opt/tomcat/latest/bin/*.sh'

sudo ln -s /usr/lib/jvm/java-8-openjdk-amd64/jre/ /usr/lib/jvm/jre

sudo vi /usr/lib/systemd/system/tomcat9.service

[Unit]
Description=Apache Tomcat Server
After=syslog.target network.target

[Service]
Type=forking
User=tomcat
Group=tomcat

Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=JAVA_OPTS=-Djava.security.egd=file:///dev/urandom
Environment=CATALINA_PID=/opt/tomcat/latest/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat/latest
Environment=CATALINA_BASE=/opt/tomcat/latest

ExecStart=/opt/tomcat/latest/bin/startup.sh
ExecStop=/opt/tomcat/latest/bin/shutdown.sh

RestartSec=30
Restart=always

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload

sudo systemctl enable tomcat9.service
sudo systemctl start tomcat9.service

sudo systemctl status tomcat9.service

cd /tmp
sudo wget --no-check-certificate https://build.geo-solutions.it/geonode/geoserver/latest/geoserver-2.18.3.war
sudo mv geoserver-2.18.3.war /opt/tomcat/latest/webapps/geoserver.war

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
        
sudo nginx -t
sudo systemctl restart nginx
