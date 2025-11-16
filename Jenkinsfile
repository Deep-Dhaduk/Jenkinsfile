pipeline {
  agent any

  stages {
    stage('Build') { steps { bat 'echo Windows build & ver & dir' } }
    stage('Test') {
      steps {
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
    success  { echo 'SUCCESS: all good 🎉' }
    unstable { echo 'UNSTABLE: tests had issues' }
    failure  { echo 'FAILURE: check Console Output' }
    changed  { echo 'STATE CHANGED since last run' }
  }
}
