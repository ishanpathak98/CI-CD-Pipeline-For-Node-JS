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

```
sudo apt update
sudo apt install openjdk-11-jdk -y


#### Verify the installation:

java -version

#### Install Jenkins

    Add the Jenkins Repository:

    

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

#### Update the package list:

sudo apt update

#### Install Jenkins:



    sudo apt install jenkins -y

3. Start and Enable Jenkins

    Start Jenkins:

    

sudo systemctl start jenkins

Enable Jenkins to start on boot:



sudo systemctl enable jenkins

Check the status of Jenkins:



    sudo systemctl status jenkins

4. Install Docker Pipeline Plugin in Jenkins

    Log in to Jenkins.
    Go to Manage Jenkins > Manage Plugins.
    In the Available tab, search for "Docker Pipeline".
    Select the plugin and click the Install button.
    Restart Jenkins after the plugin is installed.

5. Docker Installation

    Update the package list:

    

sudo apt update

Install Docker:



sudo apt install docker.io

Grant Jenkins and Ubuntu users permission to the Docker daemon:



    sudo su -
    usermod -aG docker jenkins
    usermod -aG docker ubuntu
    systemctl restart docker

    Restart Jenkins:

    Navigate to http://<ec2-instance-public-ip>:8080/restart to restart Jenkins from the web interface.

Conclusion

We have successfully set up Jenkins and Docker on our EC2 instance, and configured it to be ready for creating a CI/CD pipeline for your Node.js Todo app.

