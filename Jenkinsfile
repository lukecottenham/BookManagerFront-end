pipeline {
    agent any
    stages {
        stage('--docker-build--') {
        	steps {
        		sh "docker build -t lukecottenham/book-front-end:$BUILD_NUMBER -t lukecottenham/book-front-end:latest ."
        	}
        }
        stage('--dockerhub-push--') {
        	steps {
        		withDockerRegistry([ credentialsId: "luke-docker", url: "" ]) {
        			sh "docker push lukecottenham/book-front-end:$BUILD_NUMBER"
        			sh "docker push lukecottenham/book-front-end:latest"
        		}
        	}
        }
        stage('--test-deploy--') {
            steps {
            	sh "ssh -T -i /home/jenkins/Project.pem ubuntu@ec2-3-8-164-213.eu-west-2.compute.amazonaws.com ./docker-front-end.sh"
            }
        }
        stage('--selenium-test--') {
        	steps {
        		sh "ssh -T -i /home/jenkins/Project.pem ubuntu@ec2-3-8-164-213.eu-west-2.compute.amazonaws.com ./selenium-test.sh"
        	}
        }
    }
}
