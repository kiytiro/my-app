pipeline {
    agent any

    stages {
        stage('---read pom.xml file---') {
            steps {

                
              script {

                   def pomFile = readFile('pom.xml')

                   def pom = new XmlParser().parseText(pomFile)

                   def sonarURL =  pom['profiles'].text().trim()

                   // check for string that contains the sonar URL
//                   def sonar_URL = sonarURL.substring(sonarURL.indexOf('http'))
                   env.SONAR_HOST_URL = sonarURL.substring(sonarURL.indexOf('http'))
//echo "Sonar URL: ${sonarURL}"
//echo "The sonar URL ----------    ${sonar_URL}"
//println(sonarURL.length())

              }
            }
        }

//        stage('---display parameters---') {
//            steps {
//                echo "-------------------------------------"
//                echo "${JOB_NAME} Job Name "
//                echo "${JENKINS_HOME} Jenkins home "
//                 echo "${HOME} Jenkins HOME**** "
//                echo "${WORKSPACE} Jenkins workspace ****** "
//                echo "-------------------------------------"
//            }
//        }
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
                echo "${WORKSPACE} Jenkins workspace ****** "
                echo "Sonar URL :  ${SONAR_HOST_URL}"                
                echo "-------------------------------------"
               sh "python3 /home/labuser/pythonScripts/CheckSonarQubeQualityGate.py ${WORKSPACE} ${SONAR_HOST_URL}"  
            }
        }
    }
}
