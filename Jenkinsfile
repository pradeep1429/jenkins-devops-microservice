pipeline {
    agent any
    //agent{docker{image 'maven:3.8.1'}}
    environment{
        dockerHome = tool 'MyDocker'
        mavenHome = tool 'MyMaven'
        path = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
        stages{
            stage('Checkout'){
                steps{
                    sh 'mvn --version'
                    sh 'docker --version'
                    echo "Path - $PATH"
                    echo "BuildNo - $env.BUILD_NUMBER"
                    echo "BuildID - $env.BUILD_ID"
                    echo "BuildTag - $env.BUILD_TAG"
                    echo "JobName - $env.JOB_NAME"

                }
            }
            stage('Compile'){
                steps{
                    sh "mvn clean compile"
                }
            }
            stage('Test'){
                steps{
                    sh "mvn test"
                }
            }
            stage('IntegrationTest'){
                steps{
                    sh "mvn failsafe:integration:test failsafe:verify"
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
