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
        stage('create secret') {
            steps {
                script {
                    sh 'oc create secret.yaml'
		       }             
            }
        }
        stage('create volume') {
            steps {
                script {
                    sh 'oc create createvolume.yaml'
		       }   
            }
        }		
        stage('Deploy to Development') {
            steps {
                script {
                    sh 'oc create deployment.yaml'
		       }     
            }
        }
        stage('create Service') {
            steps {
                script {
                    sh 'oc create serviceword.yaml'
		       } 
            }
        }		
    }
}
