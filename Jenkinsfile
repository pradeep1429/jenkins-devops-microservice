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
                    sh "mvn failsafe:integration-test failsafe:verify"
                }
            }
            stage('Package'){
                steps{
                    sh "mvn package -DskipTests"
                }
            }
            stage('Build Docker Image'){
                steps{
                    script{
                        dockerImage = docker.build("deepindock/currency-exchange-devops:${env.BUILD_TAG}")
                    }
                }
            }
            stage('Push Docker Image'){
                steps{
                    script{
                        docker.withRegistry('','dockerhub'){
                            dockerImage.push();
                            dockerImage.push('latest');
                        }
                    }
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
