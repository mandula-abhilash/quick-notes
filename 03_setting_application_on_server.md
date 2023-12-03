Setting up MERN application on remote server

##### 1. Clone repository

Ex: `git clone https://github.com/username/application.git`

##### 2. Install dependencies
```

pm2 stop all	
pm2 delete all
pm2 flush

cd frontend/
npm install
npm run build

pm2 serve build 3000 --name "client"



// pm2 start node_modules/react-scripts/scripts/start.js --name "client" -- before nodejs v19
```

[pm2 cheat sheet](https://devhints.io/pm2)

#### 3. Create .env file and add production environment values

#### 4. Run express server using PM2
```
cd backend/
npm install

// Only flush the queues if needed
// pm2 start npm --name "bullmq-queues-flush" -- run flush:bullmq-queues

pm2 start npm --name "pdf-gen-worker" -- run start:pdf-gen-worker
pm2 start npm --name "pdf-gen-worker" -- run start:reg-req-worker

// pm2 monit  # Monitor all processes
// pm2 logs pdf-gen-worker  # View logs of the worker process

pm2 start server.js --name "server" -i 5 // for 5
pm2 start server.js --name "server" -i max // for max

```
