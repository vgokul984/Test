pipeline {
    agent any
    environment {
        GIT_REPO="https://github.com/vgokul984/Test.git"
        GIT_BRANCH="master"
	DEV_PROJECT = "development"
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
                    sh 'oc create -f secret.yaml'
		       }             
            }
        }
        stage('create MySQl_volume') {
            steps {
                script {
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/Mysql_deployment.yaml -n ${DEV_PROJECT}'
		       }   
            }
        }		
        stage('Deploy to MYSQLDevelopment') {
            steps {
                script {
                    sh 'oc create -f  ${DEV_PROJECT}/${ENV}/Mysql_deployment.yaml -n ${DEV_PROJECT}'
		       }     
            }
        }
        stage('create MYSQLService') {
            steps {
                script {
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/Mysql_serviceword.yaml -n ${DEV_PROJECT}'
		       } 
            }
        }
        stage('create wordpress_volume') {
            steps {
                script {
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/wordpress_volume.yaml -n ${DEV_PROJECT}'
                       }
            }
        }
        stage('Deploy to wordprss_Development') {
            steps {
                script {
                    sh 'oc create -f  ${DEV_PROJECT}/${ENV}/wordpress_deployment.yaml -n ${DEV_PROJECT}'
                       }
            }
        }
        stage('create wordpress_Service') {
            steps {
                script {
                    sh 'oc create -f ${DEV_PROJECT}/${ENV}/wordpress_service.yaml -n ${DEV_PROJECT}'
                       }
            }
        }
        stage('create route_wordpress_Service') {
            steps {
                script {
                    sh 'oc expose service wordpress --port=80 -l name=wordpress -n ${DEV_PROJECT}'
                       }
            }
        }
    }
}
