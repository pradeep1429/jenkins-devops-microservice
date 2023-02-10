pipeline {
    agent any
    //agent{docker{image 'maven:3.8.1'}}
    environment{
        dockerHome = tool 'MyDocker'
        mavenHome = tool 'MyMaven'
        path = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
        stages{
            stage('Build'){
                steps{
                    sh 'mvn --version'
                    sh 'docker --version'
                    echo "Prepare Tests to run"
                }
            }
            stage('RunTests'){
                steps{
                    echo "Run tests"
                }
            }
            stage('PublishReports'){
                steps{
                    echo "Publish Reports"
                }
            }
            stage('AggregateReports'){
                steps{
                    echo "Aggregate Reports"
                }
            }
        }
        post{
            always{
              echo 'this print always'
            }
            success{
              echo 'BUILD SUCCESS'
            }
            failure{
              echo 'BUILD FAILURE'
            }

        }


}
