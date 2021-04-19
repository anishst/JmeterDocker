#!groovy

pipeline {
    agent any
    stages {

        stage('Java App Code') {

            steps {
                echo " *****************   Checking out Code.... *****************${env.WORKSPACE}"
                dir('app') {
                    // checkout code
                    git branch: 'main', url: 'https://github.com/anishst/JavaSpringBoot.git'
                }
            }
        }

        stage('Build App') {
            agent {
                dockerfile {
                    dir './app'
                }
            }
            steps {
                    echo " *****************   Buidling APP *****************${env.WORKSPACE}"
                    sh "pwd"
                    sh "ls"
                    sh "ls -R"
            }
        }

        stage('Jmeter') {
            agent {
                dockerfile {
                    dir './jmeter'
                }
            }
            steps {
                sh 'jmeter --version'
                echo "${env.WORKSPACE}"
                sh "pwd"
                sh "ls"
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
                perfReport '**/*.jtl'

            }
        }

    }
    post { 
        always { 
            echo 'Publishing reports...'
                echo "${env.WORKSPACE}"
                sh "pwd"
                sh "ls"
            //  below command shows jtl in the artifact area
            // archiveArtifacts 'scripts/*.jtl'

            // archive perf test results; https://www.jenkins.io/doc/pipeline/steps/performance/
            //perfReport '**/*.jtl'
            
        }
    }
}
