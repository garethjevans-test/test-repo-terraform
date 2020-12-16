pipeline {
  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '10'))
    timeout(time: 30, unit: 'MINUTES')
    disableConcurrentBuilds()
  }

  stages {
    stage('Dummy') {
      steps {
        sh 'echo "Do Nothing..."'
      }
    }
  }
}
