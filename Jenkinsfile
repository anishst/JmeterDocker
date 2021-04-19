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
                //      -n [This specifies JMeter is to run in non-gui mode]
                //      -t  [name of JMX file that contains the Test Plan]
                //       -l  [name of JTL file to log sample results to]
                sh 'jmeter -n -f -t ./scripts/CSVSample.jmx -l ./scripts/CSVSample.jtl -e -o .scripts/reports/'
            }
        }

    }
}