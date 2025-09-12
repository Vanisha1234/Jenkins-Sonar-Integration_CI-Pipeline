# JENKINS - SONARQUBE INTEGRATION THROUGH CI PIPELINE
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
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
# [PROJECT SET_UP]

# Setting up Docker On Ubuntu Virtual Machine (Step-By-Step Guide)
> Ubuntu Version : Ubuntu 24.04.3 LTS \
> Commands used:
  1. sudo apt-get update
  2. sudo apt install docker.io
  3. sudo systemctl enable docker
  4. sudo systemctl status docker
  > # Docker service is running!    
  <img width="961" height="234" alt="DockerStatus" src="https://github.com/user-attachments/assets/e6066f81-5c70-43d0-9404-408e909e8605" />

# Setting up Jenkins through Docker Container (Step-By-Step Guide)
> Jenkins image used via Docker Hub : https://hub.docker.com/r/jenkins/jenkins
> Commands used:
  1. mkdir /var/jenkins_home
  2. chmod 777 /var/jenkins_home
  3. sudo docker run -d --name jenkins -p 8090:8080 -p 50000:50000 -v /var/jenkins_home:/var/jenkins_home jenkins/jenkins:lts
  4. sudo docker logs jenkins
     > This command lists the temporary password only once to unlock Jenkins
     <img width="1278" height="668" alt="setup-jenkins-02-copying-initial-admin-password" src="https://github.com/user-attachments/assets/a7f55ee9-713f-4404-91fd-6e4ed0d0e567" />

  5. Browse Jenkins using the following URL : http://localhost:8090/
     
     <img width="1598" height="1146" alt="UnlockJenkins" src="https://github.com/user-attachments/assets/483b26f8-2302-4356-bc07-94050f1bdb72" />

  7. Update the password and set up Jenkins by installing suggested plugins.
  >  # Jenkins is running!

  <img width="885" height="456" alt="manage-jenkins" src="https://github.com/user-attachments/assets/951feb15-70ea-45fc-a365-36481c74e369" />

# Setting up SonarQube & PostgreSQL through Docker Compose (Step-By-Step Guide)
> SonarQube image used via Docker Hub : https://hub.docker.com/_/sonarqube \
> Postgres image used via Docker Hub : https://hub.docker.com/_/postgres
     

        

  
     
























