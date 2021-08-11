pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        sh '''git --version'''
      }
    }
  /*agent {
    docker { 
      image 'node:12.16.2'
    } 
  }
  stages {
    stage('Build') {
      steps {
        sh 'node --version'
        sh 'npm install'
        sh 'npm run build'
      }
    }
    stage('Test') {
      parallel {
        stage('Static code analysis') {
            steps { sh 'npm run-script lint' }
        }
        stage('Unit tests') {
            steps { sh 'npm run-script test' }
        }
      }
    }*/
    stage('Deploy billing App') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'kubernete-jenkis-server-account', variable: 'api_token')
                      ]) {
            sh 'kubectl --token $api_token --server https://192.168.49.2:8443 --insecure-skip-tls-verify=true apply -f deployment-billing-app-front-jenkins.yaml '
          }

        }
      }

    }
  }