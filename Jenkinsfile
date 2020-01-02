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
                    openshift.withCluster() {
					   openshift.withProject() {
					     openshift.create(secret.yaml)
						}
					}
				}             
            }
        }
        stage('create volume') {
            steps {
                script {
                    openshift.withCluster() {
					   openshift.withProject() {
					     openshift.create(createvolume.yaml)
						}
					}
				}   
            }
        }		
        stage('Deploy to Development') {
            steps {
                script {
                    openshift.withCluster() {
					   openshift.withProject() {
					     openshift.create(deployment.yaml)
						}
					}
				}   
            }
        }
        stage('create Service') {
            steps {
                script {
                    openshift.withCluster() {
					   openshift.withProject() {
					     openshift.create(deployment.yaml)
						}
					}
				}
            }
        }		
    }
}
