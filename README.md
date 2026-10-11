# 🚀 Node.js (Express) Application Deployment on AWS EC2 with PM2



# 📖 Introduction



This project is a simple Node.js web application built with Express and deployed on an AWS EC2 instance. The application runs on port 3000 and returns a response in the browser when the server's public IP is opened.
The code is pulled from GitHub onto the EC2 server, dependencies are installed with npm, and the app is kept running in the background with PM2, a production process manager for Node.js.
The goal of this project is to practice deploying a Node.js application on the AWS cloud, from launching the server and opening the required port to verifying the live output in the browser.




# 🛠️ Technologies Used Technology Purpose

AWS EC2 (t3.micro) - Cloud server to host the application



Node.js (v18) - JavaScript runtime for the backend



Express.js - Web framework used to create the server and routes



npm - Package manager to install dependencies



PM2 - Process manager to keep the app running 24/7



Git & GitHub - Version control and code hosting

# 🏗️ Architecture Diagram (AWS)





<img width="1280" height="720" alt="WhatsApp Image 2026-10-11 at 16 30 16" src="https://github.com/user-attachments/assets/0a039118-9f3b-4e5f-83fa-dd6667180094" />


Flow: User (Browser) → Internet → Security Group (port 3000) → Express app running under PM2 on EC2 → Response back to the browser.


The code comes from GitHub using git clone, and the express package is installed using npm install.


# ⚙️ Setup & Installation (on EC2 Server)
1. Launch an EC2 instance
AMI: Amazon Linux
Instance type: t3.micro
Security Group inbound rules:
SSH (22)
Custom TCP (3000) for the Node.js app
2. Connect to the server using SSH
ssh -i my-key.pem ec2-user@<EC2-PUBLIC-IP>
3. Update the server and install Git & Node.js
sudo yum update -y
sudo yum install git nodejs -y
4. Verify the installation
node --version
npm --version
git --version
5. Clone the project from GitHub
git clone 
cd node-js-project
ls
# README.md  app.js  package.json
6. Install dependencies
sudo npm install
Without this step, running the app gives the error Cannot find module 'express'.
npm install reads package.json and installs Express and its dependencies into node_modules/.
7. Run the application
node app.js
# App listening at http://localhost:3000
8. Keep the app running in the background with PM2
node app.js stops as soon as the terminal is closed. PM2 solves this.
sudo npm install -g pm2
sudo pm2 start app.js
sudo pm2 list
9. Open in the browser
http://<EC2-PUBLIC-IP>:3000
📦 Packages Installed on the Server
Package
Installed using
Use
git
yum
Clone the project from GitHub
nodejs (v18) and npm
yum
Run JavaScript on the server and manage packages
express (+ dependencies, 68 packages in total)
npm install
Web framework for the app
pm2
npm install -g pm2
Run the app in the background and restart it on failure
📥 Input
The user opens the EC2 public IP with port 3000 in the browser. This sends an HTTP GET request to the / route of the Express app.
http://<EC2-PUBLIC-IP>:3000
Server side: installing dependencies and starting the app
The first run failed because express was missing. After sudo npm install (68 packages added, 0 vulnerabilities), the app started successfully on port 3000.
�
Load image
Running the app with PM2
PM2 starts app.js as a background process and shows its status as online.
�
Load image
📤 Output
The Express app responds with a text message, which is displayed in the browser:
�
Load image
📁 Project Structure
node-js-project/
├── app.js          # Express server (listens on port 3000)
├── package.json    # Project info and dependencies
├── README.md       # Project documentation
└── images/         # Screenshots and architecture diagram
🧩 Challenges Faced
Problem
Solution
Error: Cannot find module 'express'
Ran sudo npm install to install the missing dependencies
App stops when the terminal is closed
Used PM2 to run it as a background process
Page not opening in the browser
Added a Custom TCP rule for port 3000 in the Security Group
✅ Conclusion
In this project, a Node.js application built with Express was successfully deployed on an AWS EC2 server. The code was cloned from GitHub, dependencies were installed with npm, and the application was kept running with PM2. The output in the browser confirms that the server, the Security Group rules and the application all work correctly.
Through this project I learned:
Launching an EC2 instance and opening a custom port in the Security Group
Installing Node.js, npm and Git on a Linux server
Fixing a missing-module error using npm install
Running a Node.js app as a background process with PM2
Future improvements: add Nginx as a reverse proxy on port 80, enable HTTPS with SSL, use pm2 startup so the app restarts automatically after a server reboot, and automate deployment with a CI/CD pipeline (Jenkins / GitHub Actions).
👤 Author
Your Name
GitHub | LinkedIn
