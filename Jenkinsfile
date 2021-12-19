pipeline{

	agent { any }

	environment {
		DOCKERHUB_CREDENTIALS=credentials('capstone-dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/kevmacp/Capstone.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t kevmacp/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push kevmacp/nodeapp_test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
