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
        stage('---run python---') {
            steps {
                sh "python3 test.py arg1 arg2 arg3}"
                sh "python3 test.py ${params.Sonar_IP} ${params.Sonar_URL}"
            }
        }
    }
}

