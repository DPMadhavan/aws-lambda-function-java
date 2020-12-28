pipeline {
	environment{
		BRANCH_NAME= "${env.BRANCH_NAME}"
	}
    agent any
    stages {
        stage('Clone Repo and Clean it') {
            steps {
		    echo "${BRANCH_NAME}"
                // Get some code from a GitHub repository
                sh 'rm -rf aws-lambda-function-java'                
                sh 'git clone https://github.com/DPMadhavan/aws-lambda-function-java.git'
            }
        }
		stage('clean') {
            steps {
                sh "mvn clean"
            }
        }
		
	/*	stage('SonarQube analysis') {
			steps {
				withSonarQubeEnv('SonarQube') {
				sh 'mvn clean package sonar:sonar'
			}
		}
	}

	    stage("Quality Gate") {
            steps {
		    sleep(10)
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
		stage('Production') {
			when {
				expression { BRANCH_NAME =='main'}
			}
            	steps {
                	sh "mvn package"
					
					timeout(time:5, unit:'DAYS') {
					input message:'Approve deployment?', submitter: 'milan'
					}
					sh "aws s3 cp target/demo-1.0.0.jar s3://haeron-storage"
					sh '''aws lambda update-function-code --function-name myspringboot \\
					--s3-bucket haeron-storage \\
					--s3-key demo-1.0.0.jar \\
					--region ap-south-1'''

            }
				post{
					success{
						echo "Successfully deployed to Production"
					}
					failure{
						echo "Failed deploying to Production"
					}
				}
        }
		
		stage('Stagging') {
			when {
				expression { BRANCH_NAME =='test'}
			}
            	steps {
                	sh "mvn package"
					timeout(time:5, unit:'DAYS') {
					input message:'Approve deployment?', submitter: 'milan'
					}
					sh "aws s3 cp target/demo-1.0.0.jar s3://haeron-storage"
					sh '''aws lambda update-function-code --function-name myspringboot \\
					--s3-bucket haeron-storage \\
					--s3-key demo-1.0.0.jar \\
					--region ap-south-1'''

            }
				post{
					success{
						echo "Successfully deployed to Stagging"
					}
					failure{
						echo "Failed deploying to Stagging"
					}
				}
        } */
		
		stage('AWS Development') {
			/*when {
				expression { BRANCH_NAME =='master' | BRANCH_NAME =='dev'}
			}*/
            	steps {
                	sh "mvn package"
			
					sh "aws s3 cp target/lambda-java-api-example-1.0-SNAPSHOT.jar s3://deepatestb"
					sh '''aws lambda update-function-code --function-name deepapi \\
					--s3-bucket deepatestb \\
					--s3-key demo-1.0.0.jar \\
					--region ap-south-1'''

            }
				post{
					success{
						echo "Successfully deployed to AWS Development"
					}
					failure{
						echo "Failed deploying to Development"
					}
				}
        }
		
    }
}

