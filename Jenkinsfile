pipeline {
   agent any
   tools{
       jdk 'JDK 1.8'
       maven "maven3"
   }
   options {
       timestamps()
       buildDiscarder(logRotator(artifactDaysToKeepStr: '10', artifactNumToKeepStr: '10', daysToKeepStr: '10', numToKeepStr: '10'))
   }
 stages {
     stage ('Display PATH of Jenkins'){
         steps {
             sh '''
             echo "This is Declarative pipeline for building ServiceApp"
             echo "PATH = ${PATH}"
             '''
         }
     }
     stage ('Checkout the Source Code') {
        steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '8fa98484-5dcc-4b90-a9f8-7f4fa5dfbc20', url: 'https://github.com/kbr332github/Service-App.git']]])
         
        }
    }
      stage ('Building the Souce using Maven') {
          steps {
              sh 'mvn clean compile install'
          }
      }
      stage ('Archive artifacts for ServiceApp'){
          steps{
              archiveArtifacts '**/**/*.war'
          }
      }
      }
}
