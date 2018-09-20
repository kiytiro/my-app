# my-app
This is a maven project used to test Jenkins pipeline project.

Added the 'mvn sonar:sonar' option into the pom.xml file

The Jenkinsfile defines and sets the parameters. The parameters are used to pass as arguments to call the python script.

The Jenkinsfile calls the SonarQube, and then call a python script to evaluate the SonarQube result.
