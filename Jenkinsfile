pipeline{
	agent any
	stages{
		stage('Checkout'){
			steps{
				git branch: "main", url: 'https://github.com/Pratham232/g3-allergy-service.git'
			
			}
			
		}
		
		stage('Build'){
			steps{
				sh 'chmod a+x mvnw'
				sh './mvnw clean package -DskipTests=true' 
			}
			
			post{
				always{
					archiveArtifacts 'target/*.jar'
				}
			}
		}
      stage('DockerBuild') {
            steps {
                sh 'docker build -t itsmepratham23/g3-allergy-service:latest .'
            }
        }
        stage('Login') {

			steps {
				sh 'echo Pratham@23 | docker login -u itsmepratham23 --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push itsmepratham23/g3-allergy-service'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}
   }

