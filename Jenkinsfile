pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'newman run https://www.getpostman.com/collections/631643-f695cab7-6878-eb55-7943-ad88e1ccfd65-JsLv' 
            }
        }
    }
}