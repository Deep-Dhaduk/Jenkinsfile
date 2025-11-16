pipeline {
  agent { docker { image 'maven:3.9.11-eclipse-temurin-21-alpine' } }
  stages {
    stage('Build') {
      steps {
        sh 'mvn --version'            // step 1
        sh 'echo "Listing workspace"' // step 2
        sh '''
          echo "Multiline shell works too";
          ls -lah
        '''                           // step 3 (multiline)
      }
    }
  }
}
