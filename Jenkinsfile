@Library('ws_jenkins_commons_staging') _
pipeline {
                          agent {label 'slavedemo'}
tools {
        maven 'apache-maven-3.0.5'
        jdk 'LINUX_JDK'
      }
    stages {
            // stage('Cleanup and Checkout code') {
            //   steps {
            //           deleteDir()
            //           checkout([$class: 'GitSCM', branches: [[name: '*/branch1']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/adirgit84/java-maven-junit-helloworld']]])

            //           }
            //                                   }
                        stage('Bump version') {
              steps {
                sh 'mvn build-helper:parse-version versions:set -DnewVersion=\\${parsedVersion.majorVersion}.\\${parsedVersion.minorVersion}.\\${parsedVersion.nextIncrementalVersion} versions:commit'
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

                /*    uploadFilesToArtifactory("ui-config.${version}", "ws-maven/adir/example/")*/
              uploadFilesToArtifactory("*.jar", "ws-maven/adir/example/")
              
                  }
                       }
          stage('git clone') {
            steps {

                        withCredentials([usernamePassword(credentialsId: 'adir_private_github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) 
                            {
                              sh 'mvn build-helper:parse-version versions:set -DnewVersion=\\${parsedVersion.majorVersion}.\\${parsedVersion.minorVersion}.\\${parsedVersion.nextIncrementalVersion} versions:commit'
                              sh 'git status'          
                              sh 'git add pom.xml'
                              sh 'git commit -m "upgrade pom version"'
                              sh 'cat pom.xml'
                              sh "git push origin branch1"
                            }
                    }
                             }
      
      
                stage('git push') {
            steps {

                        withCredentials([usernamePassword(credentialsId: 'adir_private_github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) 
                            {
                              sh "git push origin branch1"
                            }
                    }
                             }
      
      
    }
}
