# Initial Server Setup for Debian 10

#### 1. Logging as root

`ssh root@YOUR_IP_ADDRESS` or  [using putty](https://user-images.githubusercontent.com/77572066/132045155-57bacad4-3ca9-4197-80c5-7c1631353500.png)

#### 2. Install sudo, vim
```
apt-get install sudo
sudo apt-get update
sudo apt-get install vim
```

#### 3. Creating a new user

`adduser abhilash`

#### 4. Granting Administrative Privileges

`usermod -aG sudo abhilash`

`sudo visudo`

Scroll down till the end of the /etc/sudoers file and append the mentioned below line

`abhilash ALL=(ALL) NOPASSSWD:ALL `

#### 5. Setting Up a Basic Firewall

```
apt update
apt install ufw
sudo ufw enable
ufw allow OpenSSH
```

#### 6. Logging as new user

`ssh abhilash@YOUR_IP_ADDRESS`

#### 7. Point domain name to your server's public IP Address

[DNS quick start](https://docs.digitalocean.com/products/networking/dns/quickstart/)

#### 8. Install Nginx
```
sudo apt update
sudo apt install nginx

sudo ufw allow 'Nginx HTTP'
sudo ufw status
systemctl status nginx
```

Now you can access default Nginx landing page at

`http://YOUR_IP_ADDRESS/`

Basic Nginx commands
```
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl disable nginx
sudo systemctl enable nginx
```

<!-- Certbot https://gist.github.com/bradtraversy/cd90d1ed3c462fe3bddd11bf8953a896 -->
