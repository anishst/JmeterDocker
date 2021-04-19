pipeline {
    agent { dockerfile true }
    stages {
        stage('Jmeter') {
            steps {
                sh 'jmeter --version'
                sh 'ls'
                echo "Running a sample Jmeter script..."
                // run script - this creates CSVSample.jtl as output in same dir as script
                // sh 'jmeter -n -t ./scripts/CSVSample.jmx'

                // run script with html report - 
                sh 'jmeter -n -t ./scripts/CSVSample.jmx -e -o ./scripts/reports'
            }
        }

    }
}