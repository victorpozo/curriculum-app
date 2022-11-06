pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/victorpozo/curriculum-app', branch: 'dev')
      }
    }

    stage('Log') {
      parallel {
        stage('Log') {
          steps {
            sh 'ls -la'
          }
        }

        stage('Instalación de dependencias') {
          steps {
            sh 'cd curriculum-front && npm i'
          }
        }

      }
    }
    
    stage('Front-End - Tests Unitarios') {
      steps {
        sh 'cd curriculum-front && npm i --save-dev vue-jest && npm run test:unit'
      }
    }

    stage('Build') {
      steps {
        sh '#docker build -f curriculum-front/Dockerfile -t fuze365/curriculum-front:latest .'
      }
    }

    stage('Log into Dockerhub') {
      environment {
        DOCKERHUB_USER = 'fuze365'
        DOCKERHUB_PASSWORD = 'gv1&3Ea9W##onDQAMUG&41CvZ7h1d1'
      }
      steps {
        sh '#docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

    stage('Push') {
      steps {
        sh '#docker push fuze365/curriculum-front:latest'
      }
    }

  }
}
