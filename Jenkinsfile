pipeline {
    agent any
    environment {
        GIT_REPO="https://github.com/vgokul984/Test.git"
        GIT_BRANCH="master"
	DEV_PROJECT = "deployment"
        PROJECT_NS = "development"
        ENV = "dev" 
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
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/secret.yaml -n ${PROJECT_NS}'
		       }             
            }
        }
        stage('create MySQl_volume') {
            steps {
                script {
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/Mysql_deployment.yaml -n ${PROJECT_NS}'
		       }   
            }
        }		
        stage('Deploy to MYSQLDevelopment') {
            steps {
                script {
                    sh 'oc create -f  ${DEV_PROJECT}/${ENV}/Mysql_deployment.yaml -n ${PROJECT_NS}'
		       }     
            }
        }
        stage('create MYSQLService') {
            steps {
                script {
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/Mysql_serviceword.yaml -n ${PROJECT_NS}'
		       } 
            }
        }
        stage('create wordpress_volume') {
            steps {
                script {
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/wordpress_volume.yaml -n ${PROJECT_NS}'
                       }
            }
        }
        stage('Deploy to wordprss_Development') {
            steps {
                script {
                    sh 'oc create -f  ${DEV_PROJECT}/${ENV}/wordpress_deployment.yaml -n ${PROJECT_NS}'
                       }
            }
        }
        stage('create wordpress_Service') {
            steps {
                script {
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/wordpress_service.yaml -n ${PROJECT_NS}'
                       }
            }
        }
        stage('create route_wordpress_Service') {
            steps {
                script {
                    sh 'oc expose service wordpress --port=80 -l name=wordpress -n ${PROJECT_NS}'
                       }
            }
        }
    }
}
