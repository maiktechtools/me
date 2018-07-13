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
        input(message: 'Aprobar?', submitter: 'imiguel')
      }
    }
    stage('Release') {
      steps {
        emailext(subject: 'Liberar', body: 'Liberar', to: 'isanjuan')
        input(message: 'Liberar?', submitter: 'isanjuan')
        sh 'echo "LIBERADO"'
        emailext(subject: 'Liberacion correcta', body: 'Liberacion aviso', attachLog: true, to: 'imiguel,isanjuan,desarrollo')
      }
    }
  }
}