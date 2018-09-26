pipeline {
    agent any

//    parameters { 
//        string(name: 'Sonar_URL', defaultValue: 'http://172.23.164.252:9000', description: 'Sonar URL ')
//        string(name: 'Repo_Name', defaultValue: 'ParameterQualityGate_1', description: 'Repo name ')
//    } 
    stages {
        stage('---read pom.xml file---') {
            steps {

                
              script {

            //       def sonar_url = sh "grep -o ?<=<sonar.host.url>.*?=</sonar.host.url> pom.xml"
            //      echo "${sonar_url} the sonar url"

                   def pomFile = readFile('pom.xml')
//echo "pomFile file: " + pomFile

                   def pomM = new XmlParser().parseText(pomFile)
//                     echo "pomM file: " + pomM

                   // check for line that contains the

//                   def gavMap = [:]
//                   gavMap['groupId'] =  pomM['groupId'].text().trim()
//                   gavMap['artifactId'] =  pomM['artifactId'].text().trim()
//                   gavMap['version'] =  pomM['version'].text().trim()
//                   gavMap['profiles'] =  pomM['profiles'].text().trim()
//                   gavMap['profile'] =  pomM['profile'].text().trim()
//                   gavMap['properties'] =  pomM['properties'].text().trim()

def sonarURL =  pomM['profiles'].text().trim()
// check for string that contains the sonar URL
def sonar_URL = sonarURL.substring(sonarURL.indexOf('http'))
env.SONAR_HOST_URL = sonarURL.substring(sonarURL.indexOf('http'))
echo "Sonar URL: ${sonarURL}"
echo "The sonar URL ----------    ${sonar_URL}"
println(sonarURL.length())


//gavMap['properties'] =  pomMi.properties[2].text().trim()
// gavMap['id'] = pomM['project.profiles.profile.id'].text()
 
                //   gavMap['sonar.host.url'] =  pomM['profiles'.'profile'.'properties'.'sonar.host.url'].text().trim()
//                  echo "${gavMap} the gav Map"
//             echo pomM.profiles[0].profile.properties.'sonar.host.url'.text().trim()

//             
//                echo "*******************************************************"
//                   echo "Version : " + pomM['version']
//                   def sonar_url = pomM[''profiles.properties.'sonari.host.url'']
//                   echo "Sonar URL: " + sonar_url

//                   def pom = readMavenPom file: 'pom.xml'
//                   echo "${pom.version} pom version"
//                   echo "${pom.profiles.properties.'sonar.host.url'} sonar "
                     
                     //Extract the data you needed from existing xml
                    // def xml1 = new XmlSlurper().parse(new File("pom.xml")) 
                //   def list = new XmlSlurper().parseText(pomFile)


              //    echo "list file: " + list
 //                   def sonar_host = xml1.'**'.find{it.name() == 'sonar.host.url'}
       //              def nodes = sonar_host.children()*.name()
       //              println XmlUtil.serialize(sonar_host)
//                     echo "${sonar_host} the sonar host "
//echo "${xml1.profiles.profile.properties.'sonar.host.url'} sonar ********"

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
