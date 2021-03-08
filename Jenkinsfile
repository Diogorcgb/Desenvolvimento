pipeline
{
	agent {
		label "mvn"
	}
	parameters
	{
		string(name: 'DOCKER_IMAGE', defaultValue: 'default_name', description: 'Docker image')
		string(name: 'DOCKER_CONTAINER', defaultValue: 'default_name', description: 'Docker container')
		string(name: 'PORT', defaultValue: '3000', description: 'Port')
	}

    stages
    {
		stage ('Maven'){
			steps
			{
				sh 'mvn clean package'
			}
		}
  
        stage('Docker build'){
            steps
            {
				sh "docker rmi -f ${DOCKER_IMAGE}"
				sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
		
		stage('Docker login'){
            steps
            {
				sh "docker login -u <user> -p <password> nexus:8082 ${DOCKER_CONTAINER}"
				sh "docker tag ${DOCKER_IMAGE} nexus:8082/${DOCKER_IMAGE}:latest}"
				sh "docker push nexus:8082/${DOCKER_IMAGE}:latest"
            }
        }
		
		stage('Clean up')
		{
			steps
			{
				cleanWs()
			}
		}
    }
}

//123
