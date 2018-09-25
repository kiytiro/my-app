pipeline {
    agent any


//    parameters { 
//        string(name: 'Sonar_URL', defaultValue: 'http://172.23.164.252:9000', description: 'Sonar URL ')
//        string(name: 'Repo_Name', defaultValue: 'ParameterQualityGate_1', description: 'Repo name ')
//    } 
    stages {
        stage('---read pom.xml file---') {
            steps {

//              def sonar_url = sh(script: 'grep -o (?<=<sonar.host.url>).*(?=</sonar.host.url>) pom.xml')
                
              script {
//                   def pomFile = readFile('pom.xml')
//                   def pomM = new XmlParser().parseText(pomFile)
//                     echo "pomM file: " + pomM
 //                  def gavMap = [:]
//                   gavMap['groupId'] =  pomM['groupId'].text().trim()
//                   gavMap['artifactId'] =  pomM['artifactId'].text().trim()
//                   gavMap['version'] =  pomM['version'].text().trim()
//             
                echo "*******************************************************"
//                   echo "Version : " + pomM['version']
//                   def sonar_url = pomM[''profiles.properties.'sonari.host.url'']
//                   echo "Sonar URL: " + sonar_url

//                   def pom = readMavenPom file: 'pom.xml'
//                   echo "${pom.version} pom version"
//                   echo "${pom.profiles.properties.'sonar.host.url'} sonar "
                     
                     //Extract the data you needed from existing xml
                     def xml1 = new XmlSlurper().parseText('pom.xml') 
                     def sonar_host = xml1.'**'.find{it.name() == 'sonar.host.url'}
       //              def nodes = sonar_host.children()*.name()
                     println XmlUtil.serialize(sonar_host)

              }
            }
        }

        stage('---display parameters---') {
            steps {
                echo "-------------------------------------"
//                echo "${params.Repo_Name} Repository name"
//                echo "${params.Sonar_URL} Sonar URL"
                echo "${JOB_NAME} Job Name "
                echo "${JENKINS_HOME} Jenkins home "
                 echo "${HOME} Jenkins HOME**** "
                echo "${WORKSPACE} Jenkins workspace ****** "
//                echo  "${params.Repo_Name11} Repository name11"
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
echo "${SONAR_HOST_URL} the sonar host URL"

            }
        }
        stage('---run CheckSonarQubeQualityGate.py python script---') {
            steps {
                echo "-------------------------------------"
//                echo "${params.Repo_Name} the Repo name"
//                echo "${params.Sonar_URL} Sonar URL"
                 echo "${WORKSPACE} Jenkins workspace ****** "
//                echo "Sonar URL : ${sonar_url}"                

                echo "-------------------------------------"
//                sh "python3 /home/labuser/pythonScripts/CheckSonarQubeQualityGate.py ${params.Repo_Name} ${params.Sonar_URL}"
//               sh "python3 /home/labuser/pythonScripts/CheckSonarQubeQualityGate.py ${WORKSPACE} sonar_url"  
            }
        }
    }
}
