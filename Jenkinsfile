/* @Library('ws_jenkins_commons_staging') */
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
    /*      stage('Deploy') {
            steps {
             
                withCredentials([usernameColonPassword(credentialsId: '44d6a6d0-b5db-423f-ab22-5233f778f69b', variable: 'adir')]) {
    // some block
}  

                
            } 
        }  */ 
         stage('Deploy') {
            steps {
                uploadFilesToArtifactory("ui-config.${version}.jar", "ws-maven/adir/example/${version}/")
                  }
                         }
    }
}
