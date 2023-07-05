pipeline {

  agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-credential')
	}

  stages {

    stage('Checkout Source') {
      steps {
        git url: 'https://github.com/johnkarthik142/jenkins-kubernetes-deployment.git', branch: 'main'
      }
    }

    stage('Build') {

			steps {
				sh 'docker build -t johnkarthik142/react-app .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push johnkarthik142/react-app'
			}
		}
	        stage('Deploying App to Kubernetes') {
                          steps {
                           script {
                                 kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
                                  }
                             }
                      }
	  
	}

  }


