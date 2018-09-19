pipeline {
    agent any
    properties([
        paramters ([
            string(name: 'Sonar_IP',
            defaultValue: '172.23.164.252',
            description: 'Sonar ')
        
            string(name: 'Sonar_URL',
            defaultValue: 'http://172.23.164.252:9000',
            description: 'Sonar URL')
        ]) 
    ])
    stages {
        stage('---clean---') {
            steps {
                sh "mvn clean"
            }
        }
        stage('---test---') {
            steps {
                sh "mvn test"
            }
        }
        stage('---package---') {
            steps {
                sh "mvn package"
            }
        }
    }
}

