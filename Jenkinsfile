pipeline{
	agent any
	stages{
		stage('Checkout'){
			steps{
				git branch: "main", url: 'https://github.com/Mrunal1616/allergy.git'
			
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
                sh 'docker build -t mrunalbarde/allergy:latest .'
            }
        }
        stage('Login') {

			steps {
				sh 'echo Mrunal@11112000 | docker login -u mrunalbarde --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push mrunalbarde/allergy'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}
   }

