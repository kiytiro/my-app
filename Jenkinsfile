pipeline {
    agent any
    parameters { 
        string(name: 'Sonar_IP', defaultValue: '172.23.164.252', description: 'Sonar IP ')
        string(name: 'Sonar_URL', defaultValue: 'http://172.23.164.252:9000', description: 'Sonar URL ')
    } 
    stages {
        stage('---clean---') {
            steps {
                sh "mvn clean"
                echo "-------------------------------------"
                echo "${params.Sonar_IP} Sonar IP address"
                echo "${params.Sonar_URL} Sonar URL"
                echo "-------------------------------------"
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

