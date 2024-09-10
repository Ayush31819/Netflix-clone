## Install Jenkins, Docker and Trivy on Jenkins EC2 Instance

### Install Jenkiks

1) To install jenkins, follow below steps.

```sh
vi jenkins.sh #make sure run in Root (or) add at userdata while ec2 launch

#inside jenkins.sh file
{
#!/bin/bash
sudo apt update -y
#sudo apt upgrade -y
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | tee /etc/apt/keyrings/adoptium.asc
echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list
sudo apt update -y
sudo apt install temurin-17-jdk -y
/usr/bin/java --version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
                  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
                  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
                              /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl start jenkins
sudo systemctl status jenkins
}

sudo chmod 777 jenkins.sh
./jenkins.sh    # this will installl jenkins
```

![image](https://github.com/user-attachments/assets/1399abf6-8c1f-4998-a36c-a8566cb48f98)

2) Now login into Jenkins site with "EC2 Public IP Address:8080"

3) Extract passowrd for jenkins using below commands

```sh
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![image](https://github.com/user-attachments/assets/5ce27fba-3230-459f-9dcc-b065f64c846f)

4) Unlock Jenkins using an administrative password and install the suggested plugins.

![image](https://github.com/user-attachments/assets/ae9cc14c-324e-411d-a3f9-cc2ba8ef016a)

5) Jenkins Getting Started Screen

![image](https://github.com/user-attachments/assets/89b6f1b5-f74f-4711-83ad-97e568a96856)

B) Insstall Docker

1) Install Docker using below commands

```sh
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker ubuntu   #my case is ubuntu
newgrp docker
sudo chmod 777 /var/run/docker.sock
```

![image](https://github.com/user-attachments/assets/3e32e861-8f0a-4580-9b04-8f251197719f)

2) After the docker installation, we create a sonarqube container (Remember to add 9000 ports in the security group).

```sh
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```

![image](https://github.com/user-attachments/assets/6a3efb4a-4b50-41e2-84a0-561805ec22e7)

3) Login into sonarqube at port 9000

![image](https://github.com/user-attachments/assets/12b346ce-2edf-48f8-95ac-d748bff13bcc)

C) Install Trivy







