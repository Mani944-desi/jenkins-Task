pipeline {
  agent any

  stages {
    stage('Run Script') {
      steps {
        // Run your script and save output
        sh './hello.sh | tee build-output.txt'
      }
    }
  }

  post {
    success {
      emailext (
        to: 'manikantdevops@gmail.com',
        subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}

Console Output (first 800 lines):
${BUILD_LOG, maxLines=800}

Attached: build-output.txt
""",
        attachmentsPattern: 'build-output.txt'
      )
    }

    failure {
      emailext (
        to: 'manikantdevops@gmail.com',
        subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}

Console Output (first 500 lines):
${BUILD_LOG, maxLines=500}
""",
        attachLog: true
      )
    }

    always {
      archiveArtifacts artifacts: 'build-output.txt', allowEmptyArchive: true
    }
  }
}

