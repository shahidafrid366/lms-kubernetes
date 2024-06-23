# LMS single server deployment
![image](https://eginnovations.com/blog/wp-content/uploads/2021/09/Amazon-AWS-Cloud-Topimage-1.jpg)
## REACT JS - Presentation tier
## NODE JS - Application tier
## POSTGRES - Data tier

## Sever setup
- t2.medium
- 15GB drive
- ports: 22, 80, 443, 3000 & 5432

## postgres installation
**visit**: https://www.postgresql.org/download/linux/ubuntu/
- sudo apt update
- sudo apt install curl ca-certificates
- sudo install -d /usr/share/postgresql-common/pgdg
- sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc
- sudo sh -c 'echo "deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
- sudo apt -y install postgresql
- psql -v
- sudo ss -ntpl
## postgres password setup
- sudo su - postgres
- psql
- \password
- enter your password: password
- \q
- exit
## node installation
**visit**: https://github.com/nodesource/distributions?tab=readme-ov-file#using-ubuntu-nodejs-20
- curl -fsSL https://deb.nodesource.com/setup_20.x -o nodesource_setup.sh
- sudo -E bash nodesource_setup.sh
- sudo apt-get install -y nodejs
- node -v
- npm -v
## clone the code
- git clone -b vm https://github.com/muralialakuntla3/lms-app.git
## build backend
- cd ~/lms
- cd api/
**- sudo vi .env**
  - MODE=production
  - PORT=3000
  - DATABASE_URL=postgresql://postgres:password@localhost:5432/postgres  
- npm install
- sudo npm install -g pm2
- sudo npx prisma db push
- npm run build
- pm2 start build/index.js
- sudo ss -ntpl
- curl http://localhost:3000/api
## build frontend
- cd ~/lms/webapp/
- **vi .env**
- VITE_API_URL=http://public-ip:3000/api  
- npm install
- npm run build
- sudo apt -y update
- sudo apt -y install nginx
- sudo rm -rf /var/www/html/*
- sudo cp -r ~/lms/webapp/dist/* /var/www/html
- sudo systemctl restart nginx 
