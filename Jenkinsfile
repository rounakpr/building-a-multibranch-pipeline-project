pipeline {
  agent {
        label 'cloud-admin-default-10-75-116-7'
        }
    stages {
      stage('checkout'){
          steps{
               checkout([$class: 'GitSCM', branches: [[name: '*/development']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'git@github.com:rounakpr/building-a-multibranch-pipeline-project.git']]])
               }
        }
      stage('Build') {
          steps{
              sh 'npm install'
          }
      }
      stage('Test') {
          steps{
              sh './jenkins/scripts/test.sh'
          }
      }
      stage('Deliver for development') {
        when {
          branch 'development'
      }
      steps {
            sh './jenkins/scripts/deliver-for-development.sh'
            input message: 'Finished using the web site? (Click "Proceed" to continue)'
            sh './jenkins/scripts/kill.sh'
      }
      }
      }
  }
