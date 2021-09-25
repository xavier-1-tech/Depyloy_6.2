pipeline {
  agent {
	label 'Agent_1'
	}
  stages {
    stage ('Build') {
      steps {
      sh 'rm -rf ./cypress2'
      sh '''
        npm install
	server -s build 
	'''
      }
    }
    stage ('test') {
      agent {
        label 'Agent_2'
      }
      steps {
      sh ''' 
        npm install cypress
        npm install mocha
        npx cypress run --spec ./cypress/integration/test.spec.js
        '''
      }
      post {
        always {
          junit 'results/cypress-report.xml'
        }
          
      }
    }
  }
} 
