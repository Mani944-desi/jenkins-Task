pipeline {
  agent any
  stages {
    stage('Run script') {
      steps {
        sh './hello.sh | tee build-output.txt'
      }
    }
  }
  post {
    always {
      archiveArtifacts artifacts: 'build-output.txt', fingerprint: true
    }
  }
}
