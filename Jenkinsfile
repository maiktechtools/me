pipeline {
  agent any
  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
    stage('Test') {
      steps {
        sh 'npm run test'
        emailext(subject: 'APROBAR', body: 'Por favor aprueba', attachLog: true, to: 'tester')
        input(message: 'Aprobar?', submitter: 'tester')
      }
    }
  }
}
