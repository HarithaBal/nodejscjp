pipeline {
    agent any

    stages {
        
        stage('Build') {
            steps {
                nodejs(nodeJSInstallationName: 'Nodejs'){
                    sh 'npm install'
                }
           }
        }
         stage("test & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('NodeJS-Jenkins-Sonar-Integration') {
                sh 'npm install sonar-scanner'
		 sh'npm i sonar-scanner --save-dev'
		  sh 'npm run sonar-scanner'    	
              }
            }
          }
	    stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
	    
        stage('Building image') {
      steps{
        script {
            docker.withRegistry( 'https://registry.hub.docker.com/', 'Jenkins-Docker-Integration' ){
             myImage = docker.build ("nodejsapp:latest")
            }
        }
      }
    }
  }
}
