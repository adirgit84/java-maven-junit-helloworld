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
                sh 'cat pom.xml'
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
                   sh 'git commit -m "upgrade pom version"'
                   sh "git push origin branch1"
                    }
                             }

    }
}
