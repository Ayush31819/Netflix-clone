## Install Jenkins, Docker and Trivy on Jenkins EC2 Instance

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

2) Now login into Jenkins site with <EC2 Public IP Address:8080>

3) Extract passowrd for jenkins using below commands

```sh
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![image](https://github.com/user-attachments/assets/5ce27fba-3230-459f-9dcc-b065f64c846f)

