pipeline {
  agent any
       
  stages {
        
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage("test & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('Jenkins-Sonar-Integration') {
                sh 'npm test'
              }
            }
          }
  }
}
