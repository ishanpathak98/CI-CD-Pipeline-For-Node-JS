# CI/CD Pipeline Setup for Node.js Todo App

This guide provides step-by-step instructions to set up a CI/CD pipeline for a simple Todo app built with Node.js, using Jenkins and Docker.

## Requirements

- Python 3.9
- Node.js
- React

## Setup Instructions

### 1. Launch an EC2 Instance

1. Go to AWS Console.
2. Navigate to `Instances (running) > Launch instances`.
3. Launch the instance with your preferred configurations.
4. Open port 8080 to allow access to Jenkins:
   - Go to `EC2 > Instances`.
   - Click on the instance.
   - In the bottom tabs, click on `Security > Security groups`.
   - Add inbound traffic rules to allow port 8080.

### 2. Jenkins Installation

#### Install Java

Jenkins requires Java to run. Install OpenJDK 11:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y

```
Verify the installation:

```
java -version

```
Verify the installation:

```
java -version

```
Install Jenkins

Add the Jenkins Repository:

```bash

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

```
Update the package list:

bash

sudo apt update

Install Jenkins:

bash

sudo apt install jenkins -y

3. Start and Enable Jenkins

Start Jenkins:

bash

sudo systemctl start jenkins

Enable Jenkins to start on boot:

bash

sudo systemctl enable jenkins

Check the status of Jenkins:

```bash

sudo systemctl status jenkins

```
4. Install Docker Pipeline Plugin in Jenkins

   ```
 Log in to Jenkins.
 Go to Manage Jenkins > Manage Plugins.
 In the Available tab, search for "Docker Pipeline".
 Select the plugin and click the Install button.
 Restart Jenkins after the plugin is installed.

```

5. Docker Installation

Update the package list:

```bash

```
sudo apt update

Install Docker:

```bash

sudo apt install docker.io

```
Grant Jenkins and Ubuntu users permission to the Docker daemon:

```bash

sudo su -
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker

```
Restart Jenkins:

```
Navigate to http://<ec2-instance-public-ip>:8080/restart to restart Jenkins from the web interface.
Further Steps

```
6. Configure Jenkins Job

```
    Log in to Jenkins.
    Click on New Item and select Freestyle project.
    Enter a name for your project and click OK.
    Under Source Code Management, select Git and enter your repository URL and branch name.
    Under Build, click on Add build step and select Execute shell. Enter the following commands to build and run your project:

```bash

# Navigate to your project directory

```
cd /path/to/your/project

```
# Install dependencies
```
npm install

```
# Build the project

```
npm run build

```
# Create Dockerfile

```
cat <<EOF > Dockerfile
FROM node:14
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 8000
CMD ["npm", "start"]
EOF

```
# Build Docker image

```
docker build -t nodejs-todo-app .

```
# Run Docker container

```
docker run -d -p 8000:8000 nodejs-todo-app

```
7. Automate Running App through Jenkins

To automate the running of the app through Jenkins:

```
    Go to Post-build Actions.
    Select Build other projects and enter the name of the job to trigger after the build is complete.

```
8. Set Up Webhooks and Build Triggers

```
    Go to your repository settings (e.g., GitHub).
    Navigate to Webhooks and add a new webhook.
    Enter the Payload URL as http://<ec2-instance-public-ip>:8080/github-webhook/.
    Set the content type to application/json.
    Select Just the push event and click Add webhook.

```
In Jenkins:

```
    Go to your project configuration.
    Under Build Triggers, check GitHub hook trigger for GITScm polling.
```
Conclusion

We have successfully set up Jenkins and Docker on our EC2 instance and configured it to be ready for creating a CI/CD pipeline for your Node.js Todo app.

css


This `README.md` file provides a comprehensive guide for setting up a CI/CD pipeline for a Node.js Todo app, using Jenkins and Docker on an EC2 instance, and includes the additional steps requested.


