pipeline{
        agent any
        environment {
	    app_version ='v1'
	    rollback = 'false'
	}
	stages{
            stage('Build Image'){
                steps{
		    script{
                         if (env.rollback == 'false'){
			    image = docker.build("abdinasir1/chaperoo-frontend")
                         }
		    }
		}
            }
            stage('Tag & Push Image'){
                steps{
                    script{
			if (env.rollback == 'false'){
			    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentialS
				image.push("${env.app_version}")
			    }
			}
                    }
	        }
    	   }
            stage('Delopy App'){
                steps{
                    sh "sudo docker-compose pull && sudo docker-compose up -d" run -d
                }
            }
        }    
}
