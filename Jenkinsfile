pipeline {
    agent any


    parameters { 
        string(name: 'Sonar_URL', defaultValue: 'http://172.23.164.252:9000', description: 'Sonar URL ')
        string(name: 'Repo_Name', defaultValue: 'ParameterQualityGate_1', description: 'Repo name ')
    } 
    stages {
        stage('---read pom.xml file---') {
            steps {
              echo "SONAR_SERVER = " + SONAR_SERVER
              script {
                   def pom = readMavenPom file: 'pom.xml'
                   echo "${pom.version} pom version"
                   echo "${pom.sonar.host.url} sonarqube URL"
              }
            }
        }

        stage('---display parameters---') {
            steps {
                echo "-------------------------------------"
                echo "${params.Repo_Name} Repository name"
                echo "${params.Sonar_URL} Sonar URL"
                echo "${JOB_NAME} Job Name "
                echo "${JENKINS_HOME} Jenkins home "
                 echo "${HOME} Jenkins HOME**** "
                echo  "${params.Repo_Name11} Repository name11"
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
