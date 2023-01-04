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
             browserstack(credentialsId: '6dedd844-ce9b-4bcc-bca1-3c85ad103f8c') {
                 sh 'npm install -g browserstack-cypress-cli'
                 sh 'browserstack-cypress run --sync'
             }
         }
    }
  }
}