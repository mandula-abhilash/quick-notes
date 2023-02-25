Setting up MERN application on remote server

##### 1. Clone repository

Ex: `git clone https://github.com/username/application.git`

##### 2. Install dependencies
```
cd frontend/
npm install
npm run build

pm2 serve build 3000 --name "client"

// pm2 start node_modules/react-scripts/scripts/start.js --name "client" -- before nodejs v19
```

#### 3. Create .env file and add production environment values

#### 4. Run express server using PM2
```
cd backend/
npm install

pm2 start backend/server.js --name "server" -i max

```
