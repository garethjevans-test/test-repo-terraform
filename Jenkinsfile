def terraformTemplate = """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: terraform
    image: hashicorp/terraform:0.13.5
    command:
    - cat
    tty: true
  - name: tfsec
    image: liamg/tfsec:v0.36.9
    command:
    - cat
    tty: true
"""

pipeline {
  agent {
    kubernetes {
      yaml terraformTemplate
    }
  }

  options {
    buildDiscarder(logRotator(numToKeepStr: '10'))
    timeout(time: 30, unit: 'MINUTES')
    disableConcurrentBuilds()
  }

  stages {
    stage('Dummy') {
      steps {
        sh 'echo "Do Nothing..."'
        pullRequest.comment('This PR is highly illogical..')  
      }
      container('terraform') {
        sh 'terraform init'
        sh 'terraform validate'
      }
    }
  }
}
