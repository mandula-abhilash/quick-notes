Setting up MERN application on remote server

##### 1. Clone repository

Ex: `git clone https://github.com/username/application.git`

##### 2. Install dependencies
```
cd application
npm install
cd frontend/
npm install
npm run build

pm2 start backend/server.js --name "server" -i max

cd frontend/
pm2 start node_modules/react-scripts/scripts/start.js --name "client"

```

#### 3. Create .env file and add production environment values

#### 4. Run express server using PM2
`pm2 start backend/server.js --name "server" -i max`
