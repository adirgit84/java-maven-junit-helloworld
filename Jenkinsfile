pipeline {
    agent {label 'slavedemo'}
tools {
maven 'apache-maven-3.0.5'
jdk 'LINUX_JDK'
      }
    stages {
        stage('cleanup and checkout code') {
            steps {
                deleteDir()
                checkout([$class: 'GitSCM', branches: [[name: '*/branch1']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/adirgit84/java-maven-junit-helloworld']]])

            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }
         stage('run test') {
            steps {
              sh 'mvn test'
            }
        }
          stage('package') {
            steps {
              sh 'mvn package -DskipTests'
            }
        }
    }
}
