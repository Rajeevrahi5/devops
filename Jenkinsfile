pipeline {
  agent any
  triggers { githubPush() }  // valid here

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'git@github.com:rajeevrahi5/devops.git',
            credentialsId: 'github-ssh'
      }
    }
    stage('Run') {
      steps {
        sh 'bash scripts/build.sh'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'logs/**, **/*.log', allowEmptyArchive: true
    }
  }
}