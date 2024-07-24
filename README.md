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

1. Update the package list:
   ```sh
   sudo apt update

Install Java:
sudo apt install openjdk-11-jre
Verify Java installation:
java -version
Install Jenkins

    Add the Jenkins key:
    curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
Add the Jenkins repository:
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
Update the package list:
sudo apt-get update
Install Jenkins:
sudo apt-get install jenkins
3. Launch Jenkins

    Open Jenkins in your browser:

    vbnet

http://<ec2-instance-public-ip>:8080

Unlock Jenkins:

    Locate the initial admin password at /var/lib/jenkins/secrets/initialAdminPassword.
    View the password:

    sh

        sudo cat /var/lib/jenkins/secrets/initialAdminPassword

    Use the password to unlock Jenkins.
    Install suggested plugins.
    Create Admin Credentials or skip this step. (Recommended if you plan to use the instance in the future)

4. Install Docker Pipeline Plugin in Jenkins

    Log in to Jenkins.
    Go to Manage Jenkins > Manage Plugins.
    In the Available tab, search for "Docker Pipeline".
    Select the plugin and click the Install button.
    Restart Jenkins after the plugin is installed.

5. Docker Installation

Update the package list:

    sh

sudo apt update

Install Docker:

sh

sudo apt install docker.io

Grant Jenkins and Ubuntu users permission to the Docker daemon:

sh

sudo su -
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker

Restart Jenkins:

vbnet

    http://<ec2-instance-public-ip>:8080/restart

Conclusion

You have successfully set up Jenkins and Docker on your EC2 instance, and configured it to be ready for creating a CI/CD pipeline for your Node.js Todo app.


