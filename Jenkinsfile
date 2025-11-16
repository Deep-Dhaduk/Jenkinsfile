pipeline {
  agent any
  options { skipStagesAfterUnstable() }
  environment { APP_ENV = 'staging' }

  stages {
    stage('Build') {
      steps {
        // Multiple steps on Windows
        bat 'echo Step 1: show Windows version & ver'
        bat 'echo Step 2: list workspace & dir'
      }
    }

    stage('Test') {
      steps {
        // Create a tiny artifact + a JUnit report
        bat @'
          mkdir reports 2>NUL
          mkdir build\libs 2>NUL
          echo ok> build\libs\app.txt
          > reports\junit.xml echo ^<testsuite name="demo" tests="1"^>^<testcase classname="demo" name="unit"/^>^</testsuite^>
        '@
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'build/libs/**/*', fingerprint: true
      junit 'reports/**/*.xml'
      echo 'Cleaning workspace'
      deleteDir()
    }
    success  { echo 'Pipeline Succeeded 🎉' }
    failure  { echo 'Pipeline FAILED — check console output' }
  }
}
