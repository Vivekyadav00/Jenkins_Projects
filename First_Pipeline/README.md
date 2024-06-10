Jenkins Pipeline on AWS EC2 with Docker

Project Overview
This project sets up a CI/CD pipeline using Jenkins on an Amazon EC2 instance, leveraging Docker as an agent to ensure a consistent environment. The goal is to automate the testing and build processes for both back-end and front-end parts of an application.

Environment Setup
EC2 Instance:

An Amazon EC2 instance was created and Jenkins was installed.
Jenkins was accessed via the EC2 instance's public IP on port 8080.
Jenkins Configuration:

A Jenkins user was created.
Necessary plugins for Docker and Git were installed.
Pipeline Configuration
Using Git for Pipeline Scripts:

The pipeline scripts were stored in a Git repository.
The Git repository URL and file paths were provided in Jenkins.
Pipeline Scripts:

Two pipelines were set up: one for testing and one for building the application.
Test Pipeline Script
The first pipeline, using Docker as an agent, checks the Node.js version.

groovy
Copy code
pipeline {
  agent {
    docker { image 'node:16-alpine' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'node --version'
      }
    }
  }
}
Build Pipeline Script
The second pipeline has two stages, each using Docker as an agent: one for back-end and one for front-end.

groovy
Copy code
pipeline {
  agent none
  stages {
    stage('Back-end') {
      agent {
        docker { image 'maven:3.8.1-adoptopenjdk-11' }
      }
      steps {
        sh 'mvn --version'
      }
    }
    stage('Front-end') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh 'node --version'
      }
    }
  }
}
Pipeline Execution
Test Pipeline:

A Docker container with Node.js was used to check the Node.js version.

Build Pipeline:

Back-end: A Docker container with Maven was used to check the Maven version.
Front-end: A Docker container with Node.js was used to check the Node.js version.
Container Management:

Docker containers were created for each stage and removed after use.
Advantages
Automation: The setup automates testing and builds, making development faster.
Consistency: Docker ensures the same environment is used every time.
Efficiency: Docker containers are lightweight and manage resources well.
Isolation: Each part of the pipeline runs in its own container, avoiding conflicts.
Portability: Docker containers can run anywhere Docker is supported.
Reproducibility: Docker images can be saved and reused, ensuring the environment can be exactly replicated.
Conclusion
Using Jenkins with Docker as an agent on an AWS EC2 instance automates and streamlines the testing and build processes for back-end and front-end components. This setup is efficient, consistent, and easily scalable for future needs.
