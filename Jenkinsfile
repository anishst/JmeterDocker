pipeline {
    agent { dockerfile true }
    stages {
        stage('Jmeter') {
            steps {
                sh 'jmeter --version'
                sh 'ls'
                echo "Running a sample Jmenter script..."
                sh 'jmeter -n -t ./scripts/CSVSample.jmx'
            }
        }

    }
}