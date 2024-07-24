STEPS TO CREATE AND IMPLEMENT THE COMPLETE CI/CD PIPELINE 
For demonstration purpose we are deploying A simple todo app built with Nodejs
Requirements

    Python 3.9
    Node.js
    React
First we need to clone the repository, for that purpose we need to get an EC2 instance from AWS 
Go to AWS Console>Instances(running)>Launch instances>
**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. To solve that we need to open port 8080 after creating the EC2 instance launch the instance 
EC2 > Instances > Click on in the bottom tabs -> Click on Security>Security groups
Add inbound traffic rules 
Jenkins Installation:- 
To install and run jenkins first we need to install the jave
To install jave use below command 
sudo apt update
sudo apt install openjdk-11-jre
Verify if the java is installed properly or not , use below command to verify and get the version details of java 
java -version
To install Jenkins use below command in the EC2 Terminal
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
LAUNCH JENKINS:- 
http://<ec2-instance-public-ip>:8080
Once Jenkins is launched it will ask to unlock jenkins . The location of the password will be at /var/lib/jenkins/secrets/initialAdminPassword
To view the password we can use below command in our EC2 
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Use the password to unlock jenkins 
Click on Install suggested plugins and wait for the Jenkins to Install suggested plugins
Create Admin Credentials or Skip the step .If you want to use current Jenkins instance in future as well, then it will be better to create admin user]
Jenkins Installation is Successful.
Now we need to Install the Docker Pipeline plugin in Jenkins:
(i)Log in to Jenkins.
(ii)Go to Manage Jenkins > Manage Plugins.
(iii)In the Available tab, search for "Docker Pipeline".
(iv)Select the plugin and click the Install button.
(v)Restart Jenkins after the plugin is installed.
(vi)Wait for the Jenkins to be restarted.
DOCKER INSTALLATION:- 
Run the below command to Install Docker
sudo apt update
sudo apt install docker.io
Grant Jenkins user and Ubuntu user permission to docker deamon using below command 
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
Restart Jenkins using below command 
http://<ec2-instance-public-ip>:8080/restart
The docker agent configuration is now successful.

