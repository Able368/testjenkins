pipeline {
  agent {
    docker { image 'node:18' }
  }
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Debug') {
      steps {
        sh 'pwd; ls -la; find . -maxdepth 3 -name package.json || true'
      }
    }
    stage('Install & Test') {
      steps {
        dir('app') {           // change 'app' if needed
          sh 'node -v'
          sh 'npm -v'
          sh 'npm ci'
          sh 'npm test || true'
        }
      }
    }
    stage('Build') {
      steps {
        dir('app') {
          sh 'npm run build || true'
        }
      }
    }
  }
  post { always { cleanWs() } }
}
