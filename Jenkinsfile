pipeline {
    agent any
    environment {
        GIT_REPO="https://github.com/vgokul984/Test.git"
        GIT_BRANCH="master"
	DEV_PROJECT = "development"
    }
    stages {
        stage('Get Latest Code') {
            steps {
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO}"
            }
        }
        stage('Deploy to Development') {
            steps {
                script {
                    sh 'oc delete -f deployment.yaml'
		       }     
            }
        }
        stage('create Service') {
            steps {
                script {
                    sh 'oc delete -f serviceword.yaml'
		       } 
            }
        }		
    }
}
