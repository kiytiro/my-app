def scmUrl = scm.getUserRemoteConfigs()[0].getUrl()
String determineRepoName() {
    return scm.getUserRemoteConfigs()[0].getUrl().tokenize('/')[3].split("\\.")[0]
}
pipeline {
    agent any
    parameters { 
        string(name: 'Sonar_URL', defaultValue: 'http://172.23.164.252:9000', description: 'Sonar URL ')
        string(name: 'Repo_Name', defaultValue: 'ParameterQualityGate_1', description: 'Repo name ')
    } 
    stages {
        stage('---display parameters---') {
            steps {
                echo "-------------------------------------"
                echo "${params.Repo_Name} Repository name"
                echo "${params.Sonar_URL} Sonar URL"
                echo "-------------------------------------"
            }
        }
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
        stage('---sonarqube analysis---') {
            steps {
                echo "-------------------------------------"
                echo "-------SonarQube - Running -------------"
                echo "-------------------------------------"
                sh "mvn sonar:sonar"
            }
        }
        stage('---run CheckSonarQubeQualityGate.py python script---') {
            steps {
                echo "-------------------------------------"
                echo "${params.Repo_Name} the Repo name"
                echo "${params.Sonar_URL} Sonar URL"
                echo "-------------------------------------"
                sh "python3 /home/labuser/pythonScripts/CheckSonarQubeQualityGate.py ${params.Repo_Name} ${params.Sonar_URL}"
            }
        }
    }
}
