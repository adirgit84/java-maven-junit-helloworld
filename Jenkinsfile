@Library('ws_jenkins_commons_staging') _
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
               /* uploadFilesToArtifactory("*.jar", "ws-maven/adir/example/") */
                /* echo "${env.BUILD_ID}  ${env.JENKINS_URL}" */
                /* uploadFilesToArtifactory("ui-config.${env.BUILD_ID}.jar", "ws-maven/adir/example/${env.BUILD_ID}/") */
              /* withCredentials([usernameColonPassword(credentialsId: '44d6a6d0-b5db-423f-ab22-5233f778f69b', variable: 'adir')]) */
                      {
                       uploadFilesToArtifactory("*.jar", "ws-maven/adir/example/")
                      /* uploadFilesToArtifactory("java-maven-junit-helloworld-1.0.0.jar", "ws-maven/adir/example/") */
                      } 
              
                  }
                       }
    }
}
