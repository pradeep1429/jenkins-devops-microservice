pipeline {
    agent any
        stages{
            stage('Build'){
                steps{
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
