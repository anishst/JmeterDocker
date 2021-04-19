pipeline {
    agent { dockerfile true }
    stages {
        stage('Jmeter') {
            steps {
                sh 'jmeter --v'
            }
        }

    }
}