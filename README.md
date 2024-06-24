# lms docker deployment
![image](https://nordicapis.com/wp-content/uploads/Docker-API-infographic-container-devops-nordic-apis.png)

## install docker:
- curl -fsSL https://get.docker.com -o install-docker.sh
- sudo sh install-docker.sh
- sudo usermod -aG docker ubuntu
- newgrp docker

## docker network: 

- docker network create -d bridge lmsnetwork

## Database: 
- docker container run -dt --name lmsdb -p 5432:5432 --network lmsnetwork -e POSTGRES_PASSWORD=admin123 postgres

## Backend:

- cd ~/lms-app/api
- docker build -t lms-api .
- docker login -u username   ---> to store your image in docker hub
- docker push image-name     ---> pushing your image in docker hub
- docker container run -dt --name api -p 3000:3000 --network lmsnetwork -e DATABASE_URL=postgresql://postgres:admin123@pub-ip:5432/postgres -e PORT=3000 -e MODE=local lms-api
- browse backend: pub-ip:3000/api

## Frontend:

- cd ~/lms-app/webapp
- Add backend url in .env of webapp 
- docker build -t lms-web .
- docker container run -dt --name web -p 80:80 --network lmsnetwork lms-web
