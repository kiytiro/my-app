pipeline {
    agent any
    parameters { 
        string(name: 'Sonar_IP', defaultValue: '172.23.164.252', description: 'Sonar IP ')
        string(name: 'Sonar_URL', defaultValue: 'http://172.23.164.252:9000', description: 'Sonar URL ')
        string(name: 'Repo_Name', defaultValue: 'my-app', description: 'Repo name ')
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
                sh "python3 test.py arg1 arg2 arg3"
                sh "python3 test.py ${params.Sonar_IP} ${params.Sonar_URL}"
            }
        }
        stage('---sonarqube analysis---') {
            steps {
                echo "-------------------------------------"
                echo "-------SonarQube - Running -------------"
                echo "-------------------------------------"
                sh "mvn sonar:sonar -sonar.host.url=${params.Sonar_URL"
            }
        }

        stage('---run python from drive---') {
            steps {
                sh "python3 /home/labuser/pythonScripts/testA.py ${params.Sonar_IP} ${params.Sonar_URL}"
                echo "-------------------------------------"
                echo "${params.Repo_Name} the Repo name"
                echo "${params.Sonar_URL} Sonar URL"
                echo "-------------------------------------"
                sh "python3 /home/labuser/pythonScripts/TestA.py ${params.Repo_Name} ${params.Sonar_URL}"
            }
        }

    }
}

