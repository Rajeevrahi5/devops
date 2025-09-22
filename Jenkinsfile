pipeline {
  agent any
  options { timestamps() }

  parameters {
    choice(
      name: 'SCRIPT',
      choices: 'scripts/build.sh\nscripts/test.sh\nscripts/deploy.sh',
      description: 'Which script to run'
    )
  }

  //triggers {
    // Use webhook trigger; keep this block empty if you rely on webhook only.
    // For fallback polling, uncomment:
    // pollSCM('H/5 * * * *')
    //githubPush()
  //}

  stages {
    stage('Checkout') {
      steps {
        // Choose ONE of the two "git" blocks below:

        // ----- HTTPS + PAT credentials -----
        // git branch: 'main',
        //     url: 'https://github.com/<your-username>/<your-repo>.git',
        //     credentialsId: 'github-https'

        // ----- SSH credentials -----
        git branch: 'main',
            url: 'git@github.com:rajeevrahi5/devops.git',
            credentialsId: 'github-ssh'
      }
    }

    stage('Prepare') {
      steps {
        sh 'git --version'
        sh 'chmod +x ${SCRIPT} || true'
      }
    }

    stage('Run script') {
      steps {
        sh "bash ${params.SCRIPT}"
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'logs/**, **/*.log', allowEmptyArchive: true
    }
  }
}