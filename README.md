# Overview
This repository contains a React frontend, and an Express backend that the frontend connects to.

# Objective
Deploy the frontend and backend to somewhere publicly accessible over the internet. The AWS Free Tier should be more than sufficient to run this project, but you may use any platform and tooling you'd like for your solution.

Fork this repo as a base. You may change any code in this repository to suit the infrastructure you build in this code challenge.

# Submission
1. A github repo that has been forked from this repo with all your code.
2. Modify this README file with instructions for:
* Any tools needed to deploy your infrastructure
* All the steps needed to repeat your deployment process
* URLs to the your deployed frontend.

# Evaluation
You will be evaluated on the ease to replicate your infrastructure. This is a combination of quality of the instructions, as well as any scripts to automate the overall setup process.

# Setup your environment
Install nodejs. Binaries and installers can be found on nodejs.org.
https://nodejs.org/en/download/

For macOS or Linux, Nodejs can usually be found in your preferred package manager.
https://nodejs.org/en/download/package-manager/

Depending on the Linux distribution, the Node Package Manager `npm` may need to be installed separately.

# Running the project
The backend and the frontend will need to run on separate processes. The backend should be started first.
```
cd backend
npm ci
npm start
```
The backend should response to a GET request on `localhost:8080`.

With the backend started, the frontend can be started.
```
cd frontend
npm ci
npm start
```
The frontend can be accessed at `localhost:3000`. If the frontend successfully connects to the backend, a message saying "SUCCESS" followed by a guid should be displayed on the screen.  If the connection failed, an error message will be displayed on the screen.

# Configuration
The frontend has a configuration file at `frontend/src/config.js` that defines the URL to call the backend. This URL is used on `frontend/src/App.js#12`, where the front end will make the GET call during the initial load of the page.

The backend has a configuration file at `backend/config.js` that defines the host that the frontend will be calling from. This URL is used in the `Access-Control-Allow-Origin` CORS header, read in `backend/index.js#14`

# Optional Extras
The core requirement for this challenge is to get the provided application up and running for consumption over the public internet. That being said, there are some opportunities in this code challenge to demonstrate your skill sets that are above and beyond the core requirement.

A few examples of extras for this coding challenge:
1. Dockerizing the application
2. Scripts to set up the infrastructure
3. Providing a pipeline for the application deployment
4. Running the application in a serverless environment

This is not an exhaustive list of extra features that could be added to this code challenge. At the end of the day, this section is for you to demonstrate any skills you want to show that’s not captured in the core requirement.



AWS EC2 Instance address
http://http://3.15.180.219/



## How to Deploy to AWS EC2

## Tools Used:
  1. AWS EC2

## Packages Necessary
  1. NGINX
  2. PM2
  3. 

## Steps:

Creating AWS EC2 Instance
1. Create an AWS Ubuntu EC2 instance. freetier is fine to use for the deployment.
2. Configure Security Groups to allow traffic on port 80 (HTTP) and 443 (HTTPS) and SSH
3. Download SSH Keys
4. SSH into the EC2 Instance
5. Run `sudo apt-get update` to update the packages on the instance

Download packages
1. Run `sudo apt-get install nginx` and install nginx
2. Run this shell script to install npm and node `curl -sL https://deb.nodesource.com/setup_12.x | sudo bash -`
3. Now install latest version of nodejs for ubuntu `sudo apt-get install -y nodejs`
4. Install pm2 library for us to run 2 node processes at the same time `sudo npm install pm2`


Configure Nginx default file
1. We need to configure the default file for nginx to point to the port we will be running our server on. Run the command `sudo vim /etc/nginx/sites-availible/default
and delete everything and use this as the configuration

server {
listen 80;
server_name _;

location / {
proxy_set_header X-Forwarded-For $remote_addr;
proxy_set_header Host $http_host;
proxy_pass http://172.31.38.77:3000;
}
}

Running the backend and frontent
Now we will run both the backend and the frontend at the same time, this is how we will be able to run our application.
1. git clone this repository
2. cd into the backend directory and run npm ci
3. run `sudo pm2 index.js`
4. cd into the frontend directory
5. run `npm ci` and `npm start` to start the react front end application. Now our application is built.
