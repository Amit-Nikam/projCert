pipeline {
  agent {label 'master'}
  stages {
    stage('Git Pull'){
	  steps{
	    echo "Git pull code"
		git 'https://github.com/Amit-Nikam/projCert'
	  
	  }
    }
	stage('Install Docker if not exist'){
	  steps{
	    echo "install docker on worker machine"
	    sh 'ansible-playbook -i /etc/ansible/hosts $WORKSPACE/Docker.yml'
	  }
    }
	stage('Build images and push to Docker Hub'){
	  steps{
	    withDockerRegistry(credentialsId: 'DOCKER_LOGIN', url: 'https://index.docker.io/v1/') {
              sh '''cd $WORKSPACE
                    docker build --file Dockerfile --tag docker.io/amitnikam/phpsampleapp:v$BUILD_NUMBER .
                    docker push docker.io/amitnikam/phpsampleapp:v$BUILD_NUMBER'''
         }
	  }
    }
    stage('Deploy Docker Container'){
	  steps{
	    sh 'ansible-playbook -i /etc/ansible/hosts $WORKSPACE/deployContainer.yml --extra-vars "build=$BUILD_NUMBER"'
	  }
    }
  }
}
