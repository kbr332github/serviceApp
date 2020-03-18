pipeline {
    agent any
    tools{
        maven 'Maven3'
        jdk 'JDK1.8'
    }
    options {
        timestamp()
        properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '10', artifactNumToKeepStr: '10', daysToKeepStr: '10', numToKeepStr: '10'))])
    }
 stages {
     stage ('Display PATH of Jenkins') {
         steps {
             sh '''
             echo "This is Declarative pipeline for building SeviceApp"
             echo "PATH = ${PATH}"
             '''
        }
     }
     stage (' Check out source code'){
            steps {
             checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'dfb5f223-45c2-4241-944b-f3b5422d48b9', url: 'https://github.com/kbr332github/Service-App.git']]])
        }
     }
      stage ('Build the code using Maven') {
          steps {
              sh 'mvn clean compile install'
            }
         }
        stage ('archiveArtifacts for ServiceApp'){
           steps{
                archiveArtifacts archiveArtifacts '**/**/*.war'
            }
        }
        
    }
}
