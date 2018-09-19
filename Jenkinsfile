pipeline {
    agent any
    paramters { 
        string(name: 'Sonar_IP', defaultValue: '172.23.164.252', description: 'Sonar ')
    } 
    stages {
        stage('---clean---') {
            steps {
                sh "mvn clean"
                echo "${params.Sonar_IP} Sonar IP address"
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

