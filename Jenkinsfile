def version   = '2.1.2'
pipeline{
    agent   { label 'mavenagent' }
    environment{
        PATH = "/opt/apache-maven-3.9.2/bin:$PATH"
    }
    stages{

        stage('build'){
            
            steps{
                echo 'build started'
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo 'build finsihed'
            }

        }
        stage('Unit Test'){
            steps{
                echo 'unit test started '
                sh 'mvn surefire-report:report'
                echo 'unit test completed'
            }

        }    

             stage('SonarQube analysis') {
            environment {
            scannerHome = tool 'SonarScaner'
            }
        steps { 
            echo '------------------- Sonar Started -------------'
        withSonarQubeEnv('Sonar-Server') { // If you have configured more than one global server connection, you can specify its name
            sh "${scannerHome}/bin/SonarScaner"
    }
    echo '------------------- Sonar Analysis Completed -------------'
  }
    }
   
 
 
        
        }   
    }

       


