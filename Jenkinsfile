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
        
    }
}
