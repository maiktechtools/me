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
      }
    }
    stage('Delivery') {
      steps {
        sh '''echo "Transfering files ..."
sftp -o StrictHostKeyChecking=no -b deploy.sh ${TARGET_SERVER_USER}@${TARGET_SERVER_HOST}
echo "Setup environment ..."
ssh -o StrictHostKeyChecking=no ${TARGET_SERVER_USER}@${TARGET_SERVER_HOST} \\
  \'cd me && npm install --production\'
echo "Restart services ..." 
ssh -o StrictHostKeyChecking=no ${TARGET_SERVER_USER}@${TARGET_SERVER_HOST} \\
  \'cd me && pm2 startOrRestart ecosystem.config.json --env production && pm2 save\''''
      }
    }
  }
  environment {
    TARGET_SERVER_USER = 'ec2-user'
    TARGET_SERVER_HOST = '52.15.213.43'
  }
}
