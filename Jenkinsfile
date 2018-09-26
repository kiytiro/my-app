pipeline {
    agent any

    stages {
        stage('---read pom.xml file---') {
            steps {

               // Get the SonarQube host URL from the pom.xml
               script {
                  // read the pom.xml file
                  def pomFile = readFile('pom.xml')

                  // parse the file as XML file
                  def pom = new XmlParser().parseText(pomFile)

                  // get the XML attribute that contains the SonarQube host URL
                  def sonarURL =  pom['profiles'].text().trim()

                  // check for string that contains the sonar URL and bind it for
                  // the CheckSonarQubeQualityGate python to use as a parameter
                  env.SONAR_HOST_URL = sonarURL.substring(sonarURL.indexOf('http'))
              }
            }
        }
        stage('---format project path---') {
            steps {
                env.PROJECT_PATH = '${WORKSPACE}/examples/jenkins/maven_quality_gate_example/my-app'
                echo "Project path: ${PROJECT_PATH}"
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
                echo "Jenkins Workspace:  ${WORKSPACE} "
                echo "Sonar HOST URL   :  ${SONAR_HOST_URL}"                
                echo "-------------------------------------"
               sh "python3 /home/labuser/pythonScripts/CheckSonarQubeQualityGate.py ${WORKSPACE} ${SONAR_HOST_URL}"  
            }
        }
    }
}
