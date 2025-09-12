# JENKINS - SONARQUBE INTEGRATION THROUGH CI PIPELINE

## 📑 Table of Contents
- [Project Overview](#project-overview)
- [Purpose](#purpose)
- [Tech Stack](#tech-stack)
- [Pipeline Goal](#pipeline-goal)
- [Key Highlights](#key-highlights)
- [Setup Instructions](#project-setup)
  - [Docker Setup](#setting-up-docker-on-ubuntu-virtual-machine)
  - [Jenkins Setup](#setting-up-jenkins-through-docker-container)
  - [SonarQube & PostgreSQL Setup](#setting-up-sonarqube--postgresql-through-docker-compose)
- [CI Pipeline Creation](#creation-of-ci-pipeline-step-by-step)
- [GitHub & Jenkins Integration](#integration-of-git-hub-with-jenkins-step-by-step)
- [SonarQube Integration](#integration-of-sonarqube-with-jenkins-ci-pipeline-step-by-step)
- [Results](#results)

# [PROJECT OVERVIEW]
> This set-up was developed from scratch for my organization to eliminate the challenges of time-consuming manual testing and overlooked issues by automating code testing and analysis, ensuring accuracy and timely results.

# Purpose:
> The project demonstrates the end-to-end integration of Jenkins, GitHub, and SonarQube to automate build and code quality analysis for a React.js application. The focus is on showcasing continuous integration (CI) and code analysis rather than deployment.

# Tech Stack:
1. React.js – Frontend project built with Node.js
2. Jenkins – CI server to automate pipeline stages (checkout, build, analysis) via Docker
3. GitHub – Version control and pipeline trigger via webhooks
4. SonarQube – Code quality and static analysis with quality gates
5. PostgreSQL – Database for SonarQube
6. Docker & Docker Compose – Containerized setup for SonarQube and Postgres

# Pipeline Goal:
1. Demonstrate Jenkins + SonarQube integration using a CI pipeline.
2. Automate code checkout, build, and static code analysis.
3. Highlight secure credential usage and pipeline-as-code practices.

# Key Highlights:
1. Setting up of Jenkins and SonarQube from scratch via Docker & Docker Compose file.
2. Setting up of CI pipeline for automation through Jenkins
3. Integration of Github and Jenkins
4. Integration of Jenkins and SonarQube
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
# [PROJECT SET_UP]

# Setting up Docker On Ubuntu Virtual Machine (Step-By-Step)
> Ubuntu Version : Ubuntu 24.04.3 LTS \
> Commands used:
  1. sudo apt-get update
  2. sudo apt install docker.io
  3. sudo systemctl enable docker
  4. sudo systemctl status docker
  > # Docker service is running!    
  <img width="961" height="234" alt="DockerStatus" src="https://github.com/user-attachments/assets/e6066f81-5c70-43d0-9404-408e909e8605" />

# Setting up Jenkins through Docker Container (Step-By-Step)
> Jenkins image used via Docker Hub : https://hub.docker.com/r/jenkins/jenkins
> Commands used:
  1. mkdir /var/jenkins_home
  2. chmod 777 /var/jenkins_home
  3. sudo docker run -d --name jenkins -p 8090:8080 -p 50000:50000 -v /var/jenkins_home:/var/jenkins_home jenkins/jenkins:lts
  4. sudo docker logs jenkins
     > This command lists the temporary password only once to unlock Jenkins
  <img width="1278" height="668" alt="setup-jenkins-02-copying-initial-admin-password" src="https://github.com/user-attachments/assets/a7f55ee9-713f-4404-91fd-6e4ed0d0e567" />

  5. Browse Jenkins using the following URL : http://<your-jenkins-server>:8090/
     
  <img width="1598" height="1146" alt="UnlockJenkins" src="https://github.com/user-attachments/assets/483b26f8-2302-4356-bc07-94050f1bdb72" />

  6. Updated the password and set up Jenkins by installing suggested plugins.
  >  # Jenkins is Running!

  <img width="885" height="456" alt="manage-jenkins" src="https://github.com/user-attachments/assets/951feb15-70ea-45fc-a365-36481c74e369" />

# Setting up SonarQube & PostgreSQL through Docker Compose (Step-By-Step)
> SonarQube image used via Docker Hub : https://hub.docker.com/_/sonarqube \
> Postgres image used via Docker Hub : https://hub.docker.com/_/postgres \
  To install Docker-Compose commands used:
 1. sudo apt update
 2. mkdir -p ~/.docker/cli-plugins/
 3. sudo curl -SL https://github.com/docker/compose/releases/download/v2.27.0/docker-compose-linux-x86_64 \
    -o ~/.docker/cli-plugins/docker-compose
 3. sudo chmod +x ~/.docker/cli-plugins/docker-compose
 4. Created a docker-compose file - vim docker-compose.yml \
    *Please find the docker compose file used here in the Repository*
 5. docker compose up -d 

   <img width="1205" height="140" alt="Docker-compose" src="https://github.com/user-attachments/assets/ec810a86-5dcb-4081-abe2-e07451abc8a4" />


 7. URL to access SonarQube Service : http://<your-sonarqube-server>:9001
 > # SonarQube is Running!

   <img width="1338" height="730" alt="image" src="https://github.com/user-attachments/assets/ad5f4dbe-4aff-4242-8b1f-16112b2e17f5" />

 8. Used default username & password to login - admin

# Integration of Git-hub with Jenkins (Step-By-Step)
STEP 1: Generation of personal access token on Github
 1. Github Dashboard > Your Account > Settings > Developer Settings > Personal Access Tokens > Tokens (Classic) > Generate New Token > Generate New Token (Classic) \
 2. Provided name and repository access to the token and generated a new token.
 3. Saved the generated token at a safe space.

STEP 2: Add Git generated token to Jenkins 
 1. Jenkins Dashboard > Manage Jenkins > credentials > Global > Add Credentials
    Provided Github Username, Added token as password and saved the changes

# Creation of CI Pipeline (Step-By-Step)
*Please find the Jenkinsfile file used here in the Repository*
STEP 1: Setting up NodeJs on Jenkins
 1. Jenkins Dashboard > Manage Jenkins > Manage Plugins > Available plugins > Install Node Js
 2. Manage Jenkins > Tools > Node Js > Select Version > Apply and Save to complete installation
    
STEP 2: Creating CI script for pipeline
 1. Jenkins Dashboard > New Item > Provided Item Name > Select Pipeline > Written down CI pipeline script > Save and apply > Build Now to run the pipeline
*Git credentials stored in Jenkins are already added directly in pipeline since its a private repository*

> Our Pipeline is running as expected!

<img width="726" height="128" alt="Pipeline" src="https://github.com/user-attachments/assets/ee49b028-5506-4244-8ae4-fafb8935cefa" />


# Integration of SonarQube with Jenkins CI Pipeline (Step-By-Step)
STEP 1: Installation of SonarQube for Jenkins
 1. Jenkins Dashboard > Manage Jenkins > Manage Plugins > Available plugins > Set-up SonarQube Scanner & Sonar Quality gates > Restart Jenkins by restarting the  Jenkins Container
    
STEP 2: Generation of SonarQube Token
 1. SonarQube Dashboard > Projects > Create a Project > Provided Project key name > Set up > Locally > Generated token
 2. Saved the generated token at a safe space.
 3. Under run analysis > Selected the language on which our project is based

STEP 3: Addition of SonarQube credentials in Jenkins
 1. Jenkins Dashboard > Manage Jenkins > credentials > Global > Add Credentials > kind: Secret text > Provided Secret SonarQube Token generated
 2. Manage Jenkins > System > SonarQube Servers > Provide SonarQube browsing URL and Select access token used for SonarQube > Apply and Save

STEP 4: Configurion of SonarQube with Jenkins Pipeline Script \
*Added the following block of environment Variable to the pipeline script*

<img width="947" height="99" alt="image" src="https://github.com/user-attachments/assets/824f480f-bbab-4582-9457-a2d9e9dd1282" />

> Project Key : Name of the Project created on SonarQube \
> SonarQube Scanner Path : Jenkins Dashboard > Manage jenkins > Tools > SonarQube Scanner Installations > Provided the name 


*Added the following stage to the pipeline script*

<img width="938" height="317" alt="image" src="https://github.com/user-attachments/assets/183eefb8-8f06-4e3a-b8c8-e858afe1ce1a" />


> Our Pipeline is running as expected with SonarQube Integrated!

<img width="726" height="128" alt="Pipeline2" src="https://github.com/user-attachments/assets/f07f5a6d-eea5-49b3-acba-f8e03e2d00a3" />

> SonarQube is displaying results!

<img width="795" height="214" alt="SonarQube" src="https://github.com/user-attachments/assets/fbcffe6d-75b0-44d9-9784-34583f314589" />







     

        

  
     
























