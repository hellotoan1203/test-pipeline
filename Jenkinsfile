pipeline {
  environment {
    BUILD_ID = "1"
    JENKINS_URL = "http://localhost:8080/"
    FOO = "BAR"
  }
  agent any 
  stages {
    stage('Build') {
      agent {
        docker {
          alwaysPull true args '-v /mnt:/mnt'
          image 'node:14-alpine'
        }
      }
      steps {
        echo 'Building..'
        sh ''
        ' node --version echo "I did edit it!" > README.md '
        ''
        echo " = ${env.FOO}"
      }
    }
    stage('Building our image') {
      agent {
        docker {
          alwaysPull true args '-v /var/run/docker.sock:/var/run/docker.sock:ro'
          image 'docker:20.10.8'
        }
      }
      steps {
        sh 'ls -l'
        sh 'docker build -t test/node:1.0.0 -f Dockerfile .'
        sh 'docker run --rm -t test/node:1.0.0 cat /tmp/README.md'
      }
    }
    stage('Test') {
      steps {
        echo "Testing ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'ls -l'
        sh 'cat README.md'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying....'
      }
    }
  }
}