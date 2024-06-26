# Docker-node.js-app

Technologies Used :
Docker
Docker-Compose
Docker volumes for persistent storage
AWS ECR (repo)
CI/CD Jenkins
Docker Hub

This demo app shows a simple user profile app set up using

index.html with pure js and css styles
nodejs backend with express module
mongodb for data storage

All components are docker-based

With Docker

To start the application
Step 1: Create docker network

docker network create mongo-network 


Step 2: start mongo

docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=pass --name mongo --net mongo-network mongo   


Step 3: start mongo-express

docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_SERVER=mongo -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=pass --name mongo-express --network mongo-network  -e ME_CONFIG_BASICAUTH_USERNAME=admin -e ME_CONFIG_BASICAUTH_PASSWORD=pass mongo-express  


NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit --net flag in docker run command
Step 4: open mongo-express from browser

http://localhost:8081


Step 5: create user-account db and users collection in mongo-express
Step 6: Start your nodejs application locally - go to app directory of project

npm install 
node server.js


Step 7: Access you nodejs application UI from browser

http://localhost:3000



With Docker Compose

To start the application
Step 1: start mongodb and mongo-express

docker-compose -f docker-compose.yaml up


You can access the mongo-express under localhost:8080 from your browser
Step 2: in mongo-express UI - create a new database "my-db"
Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"
Step 4: start node server

npm install
node server.js


Step 5: access the nodejs application from browser

http://localhost:3000



To build a docker image from the application

docker build -t my-app:1.0 .       


The dot "." at the end of the command denotes location of the Dockerfile.
