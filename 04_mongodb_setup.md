Install and setup mongodb on Debian 10

##### 1. Install MongoDB
```
sudo apt-get update
sudo apt install curl
curl https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/5.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list

sudo apt update
sudo apt-get install -y mongodb-org

sudo systemctl start mongod
sudo systemctl enable mongod
sudo systemctl status mongod

sudo ufw allow from YOUR_IP_ADDRESS to any port 27017
sudo ufw reload
sudo ufw status
```

#### 2. Create super user
```
mongo
use admin
db.createUser(
  {
    user: "dbAdmin",
    pwd: "str0ongHhHADdMinNPassWoRd",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
exit
```

#### 3. Enable security
`sudo vi /etc/mongod.conf`

Update 
`bindIp: 127.0.0.1` 
to 
`bindIp: 127.0.0.1,MONGO_HOST_IP_ADDRESS`

Update 
```
#security:
``` 
to 
```
security:
  authorization: "enabled"
```

```
sudo systemctl restart mongod
sudo systemctl status mongod
```

#### 4. Create read write and backup user
```
mongo -u dbAdmin -p --authenticationDatabase admin
use admin

db.createUser(
  {
    user: "applicationUser",
    pwd: "str0ongHhHApPpAssWoRd",
    roles: [{ role: "readWrite", db: "application_db" }]
  }
)

db.createUser(
  {
    user: "backupUser",
    pwd: "str0ongHhHBackUPpAssWoRd",
    roles: [{ role: "backup", db: "admin" }]
  }
)


```

To backup database:
```mongodump --username backupUser --password str0ongHhHBackUPpAssWoRd```

To restore database:
```mongorestore --username applicationUser --password str0ongHhHApPpAssWoRd```
