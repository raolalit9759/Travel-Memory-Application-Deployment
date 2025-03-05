# Travel-Memory-Application-Deployment
Travel Memory
.env file to work with the backend after creating a database in mongodb:

MONGO_URI='mongodb+srv://abhay06072002:D0fiQ4heOhotB5Wq@abhaycluster.xfyr2p6.mongodb.net/tmbatch7'
PORT=3001
Data format to be added:

{
    "tripName": "Incredible India",
    "startDateOfJourney": "19-03-2022",
    "endDateOfJourney": "27-03-2022",
    "nameOfHotels":"Hotel Namaste, Backpackers Club",
    "placesVisited":"Delhi, Kolkata, Chennai, Mumbai",
    "totalCost": 800000,
    "tripType": "leisure",
    "experience": "Lorem Ipsum, Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum, ",
    "image": "https://t3.ftcdn.net/jpg/03/04/85/26/360_F_304852693_nSOn9KvUgafgvZ6wM0CNaULYUa7xXBkA.jpg",
    "shortDescription":"India is a wonderful country with rich culture and good people.",
    "featured": true
}
Table of Contents
Project Description Technologies Used Installation Instructions Usage Deployment Load Balancing Domain Setup with Cloudflare Contributing License Acknowledgments

Project Description
The TravelMemory application is a full-stack web application built using the MERN stack (MongoDB, Express.js, React, Node.js). The purpose of this project is to allow users to document their travel experiences and memories in a user-friendly interface. This repository contains the code and configuration for deploying the application on Amazon EC2, ensuring scalability and efficient user access.

Technologies Used
Frontend: React.js Backend: Node.js, Express.js Database: MongoDB Deployment: Amazon EC2 Load Balancing: AWS Elastic Load Balancer Domain Management: Cloudflare Other Tools: Nginx, Git

Installation Instructions
Prerequisites
Node.js and npm installed on your local machine. Git installed on your local machine. An AWS account for deploying the application.

Clone the Repository
git clone https://github.com/UnpredictablePrashant/TravelMemory
Navigate to the Project Directory
cd TravelMemory/backend
Install dependencies
npm install
Configure .env file: Update the .env file with your MongoDB credentials and port details.

Start the backend
npm start
Configure Nginx as a reverse proxy
sudo nano /etc/nginx/sites-available/default
Add the following configuration

    server {
listen 80;
server_name your-ec2-public-ip;

location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
} Restart Nginx:

 sudo systemctl restart nginx
Frontend and Backend Connection
Set up the frontend
Navigate to the frontend directory

 cd ../frontend
Install frontend dependencies

npm install
Update urls.js to connect to the backend
Open urls.js in a text editor

nano src/config/urls.js
Build the frontend
npm run build
Scaling the Application
Launch additional EC2 instances
Repeat the earlier steps to launch additional EC2 instances

Set up an AWS Load Balancer
reate a new load balancer. Add the instances (frontend and backend) to the load balancer. Configure listeners to forward HTTP traffic (port 80) to EC2 instances.

Domain Setup with Cloudflare
Add domain to Cloudflare Create DNS records

Configure Nginx as a Reverse Proxy
Follow the steps outlined in previous documentation to set up Nginx as a reverse proxy for both the frontend and backend.

Load Balancing
To ensure efficient distribution of incoming traffic:

Create Multiple EC2 Instances for both frontend and backend.
Set Up an AWS Elastic Load Balancer (ELB) to manage traffic across these instances.
Add the instances to the ELB and configure health checks to ensure traffic is routed only to healthy instances.
Domain Setup with Cloudflare
Create an Account on Cloudflare and add domain.
Configure DNS Records: Create a CNAME record pointing to load balancer endpoint. Create an A record with the IP address of the EC2 instance hosting the frontend.
Contributing
Contributions are welcome!

License
This project is licensed under the MIT License. See the LICENSE file for details.

Acknowledgments
Thanks to UnpredictablePrashant for the original TravelMemory codebase.
