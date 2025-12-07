
## 🚀 GitHub Code Deployment on Apache2 Web Server by Using Jenkins (CI/CD Pipeline)

This project demonstrates a complete CI/CD workflow where Jenkins automatically pulls application source code from a GitHub repository and deploys it to an Apache2 web server. Jenkins job is triggered using a GitHub webhook, and the entire workflow runs through a Jenkins Declarative Pipeline.










## 📌 Project Overview

The purpose of this project is to implement a fully automated deployment process using Jenkins, GitHub, and Apache2

- Webhook triggers Jenkins whenever new code is pushed.
- Jenkins pulls the code from GitHub.
- Jenkins deploys the code to /var/www/html.
- Jenkins is added to the www-data group so it can manage Apache2 service actions without permission issues.
- Jenkins restarts Apache2 automatically after deployment.
- we achieve this steps through shell scripting.




## 🛠️ Technologies Used

**GitHub:** Source code repository

**Jenkins:** CI/CD automation server

**GitHub Webhook:** Triggers Jenkins pipeline

**Apache2:** Hosts the application

**shell scripting:** Node, Runs deployment

**Pipeline job:** Jenkinsfile-based automation


## ⚙️ Pre-requisites

Ensure the following before running the project:

✔ Jenkins installed and running.

✔ Apache2 installed.

✔ Jenkins user added to the www-data group.

✔ GitHub webhook configured.

✔ Jenkins plugins required

- Git Plugin



## Projects steps 

Install Jenkins , start to run  , ebable, and check status 

☕ Install Java
```bash

sudo apt install -y openjdk-17-jdk
```
⚙️ Installing Jenkins
```bash

sudo apt install -y jenkins
```
▶️ Starting Jenkins service
```bash

sudo systemctl start jenkins

```
🔄 Enabling Jenkins service
```bash

sudo systemctl enable jenkins
```

🟢 Checking Jenkins status
```bash

sudo systemctl status jenkins
```
⚙️ Install Apache2
```bash
sudo apt install -y apache2

```
▶️ Start Apache2 service
```bash
sudo systemctl start apache2
```
🟢 Apache2 Status
```bash
sudo systemctl status apache2
```
🔐 Grant Jenkins Permission to Restart Apache2.

- Apache2 runs under the www-data user, Jenkins needs permission to access /var/www/html and restart the service.
👨‍💻 Add Jenkins to www-data group
```bash

sudo usermod -aG www-data jenkins
```
🔨 change ownership of web directory
```bash
sudo chown -R www-data:www-data /var/www/
```
🛠 set proper directory permissions
```bash
sudo chmod -R 775 /var/www/
```
🛠 Restart Jenkins to apply group changes
```bash
sudo systemctl restart jenkins
```
🧠 give permission Jenkins to restart Apache2 without asking sudo password
```bash
sudo visudo

#visudo is a special, safe editor used to modify the /etc/sudoers file.
```
✍️ add rule to jenkins run systemctl command 
```bash
jenkins ALL=(ALL) NOPASSWD: /bin/systemctl restart apache2
```


    

## create a new jenkins pipeline job 

<img width="1894" height="854" alt="{54BB4AFE-3906-49AF-A26C-CE090DD1B3D7}" src="https://github.com/user-attachments/assets/55b8d7c5-5ede-40a5-947c-9a520ad48a8c" />



## Configure pipeline

```jenkinsfile
pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/selva12543/jenkins-1.git'
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                    echo "Deploying index.html to Apache..."

                    # Clean old files
                    rm -rf /var/www/html/*

                    # Copy all files
                    cp index.html styles.css /var/www/html/

                    # Restart Apache
                    sudo systemctl restart apache2.service
                '''
            }
        }
    }
    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
```


## create webhook in github 
🔄 Jenkins job will be triggered by a webhook when a developer pushes code to GitHub.

<img width="1652" height="982" alt="{39910A7C-5F0B-47CB-BF87-4AB24826BE9C}" src="https://github.com/user-attachments/assets/d185014e-5bd3-4e19-b3bc-e531d9a7da02" />


## build job 
<img width="435" height="642" alt="{4BB29456-C1C0-4ECA-9BB4-937EB32DAAE6}" src="https://github.com/user-attachments/assets/5c076b07-367f-487d-86b4-e9df774e7e8a" />

## we can see output in browser 
<img width="1907" height="1027" alt="{1D9FB89A-4045-47E5-8CF0-36DE301CCD53}" src="https://github.com/user-attachments/assets/708de5e0-9be2-4817-b342-1c36312330f4" />


## By implementing this pipeline, we will achieve

✔ Automated deployment triggered by GitHub commits.

✔ Jenkins-powered CI/CD pipeline.

✔ Automatic Apache2 restart after deployment

✔ Permission-managed integration using the www-data group

✔ Reliable validation.  








## Lessons Learned

 
By this project  complete CI/CD workflow where Jenkins automatically pulls application source code from a GitHub repository and deploys it to an Apache2 web server, and Jenkins job is triggered using a GitHub webhook. 

