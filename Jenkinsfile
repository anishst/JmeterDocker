pipeline {
    agent none
    stages {
        stage('Back-end') {
         agent {
                dockerfile {
                    dir './Dockerfile_spring'
                    label 'my-label1'
                }
            }
            steps {
                sh 'node --version'
            }
        }

        stage('Jmeter') {
            agent {
                dockerfile {
                    dir './Dockerfile'
                    label 'my-label'
                }
            }
            steps {
                sh 'jmeter --version'
                sh 'ls'
                echo "Running a sample Jmeter script..."
                // ref: https://jmeter.apache.org/usermanual/get-started.html#options
                // run script - this creates CSVSample.jtl as output in same dir as script
                // sh 'jmeter -n -t ./scripts/CSVSample.jmx'

                // run script with html report - 
                //      -n [This specifies JMeter is to run in non-gui mode]
                //      -t  [name of JMX file that contains the Test Plan]
                //       -l  [name of JTL file to log sample results to]
                //       -f force delete existing results files and web report folder if present before starting the test
                //       - j jmeter logs
                sh 'jmeter -n -f -t ./scripts/CSVSample.jmx -l ./scripts/results.jtl -e -o ./scripts/reports/ -j ./scripts/jmeter.log'
            }
        }

    }
    post { 
        always { 
            echo 'Publishing reports...'
            //  below command shows jtl in the artifact area
            // archiveArtifacts 'scripts/*.jtl'

            // archive perf test results; https://www.jenkins.io/doc/pipeline/steps/performance/
            perfReport '**/*.jtl'
            
        }
    }
}