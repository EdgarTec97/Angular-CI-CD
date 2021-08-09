pipeline {
  agent {
    docker { image 'node:10-alpine' }
  }
  stages {
    stage('Restore') {
        steps {
            sh 'npm install'
        }
    }
    stage('Build') {
        steps {
            sh 'npm run-script build'
        }
    }

    /*stage('Test') {
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