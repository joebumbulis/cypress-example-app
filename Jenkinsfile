pipeline {
  agent { 
    any { label 't1.small' }
  }

  tools { nodejs "nodejs" }

  stages {
    // first stage installs node dependencies and Cypress binary
    stage('build') {
      steps {
        // there a few default environment variables on Jenkins
        // on local Jenkins machine (assuming port 8080) see
        // https://example.cypress.io/pipeline-syntax/globals#env
        echo "Running build ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'npm ci'
        sh 'npm run cy:verify'
      }
    }

    stage('browserstack parallel tests') {

      steps {
             browserstack(credentialsId: '3e4573b5-0c1b-4809-a3d9-f84b6c4f3fcd') {
                 sh 'npm install -g browserstack-cypress-cli'
                 sh 'browserstack-cypress run --sync'
             }
         }
    }
  }
}