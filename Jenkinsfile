pipeline {
  agent { 
    any { label 't1.small' }
  }
  
  tools { nodejs "Node19Cypress" }

  stages {
    stage('build') {
      steps {
        sh 'npm ci'
        sh 'npm run cy:verify'
      }
    }

    stage('browserstack parallel tests') {
      steps {
             browserstack(credentialsId: '3e4573b5-0c1b-4809-a3d9-f84b6c4f3fcd') {
                 sh 'npm install -g browserstack-cypress-cli'
                 sh "browserstack-cypress run --sync"
             }
         }
    }
  }
}