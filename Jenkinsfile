pipeline {
    agent {label 'slavedemo'}
tools {
maven 'apache-maven-3.0.5'
jdk 'LINUX_JDK'
      }
    stages {
        stage('Cleanup and Checkout code') {
            steps {
                deleteDir()
                checkout([$class: 'GitSCM', branches: [[name: '*/branch1']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/adirgit84/java-maven-junit-helloworld']]])

            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
         stage('Run test') {
            steps {
              sh 'mvn test'
            }
        }
          stage('Package') {
            steps {
              sh 'mvn package -DskipTests'
            }
        }
          stage('Deploy') {
            steps {
              sh 'mvn deploy'
            }
        }        
    }
}
