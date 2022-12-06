pipeline {
    agent any
    stages {  
        stage("Cloning Project"){
            steps {
                git branch: 'master',
                url: 'https://github.com/riadh70/Devops_Project.git'
                echo 'checkout stage'
            }
        }
       
          agent { label 'linux' }
         options {
         buildDiscarder(logRotator(numToKeepStr: '5'))
            }
        stages {
        stage('Scan') {
         steps {
        withSonarQubeEnv(installationName: 'sq1') { 
          sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
            }
          }
        }
      }
       
         stage("SonarQube Analysis") {
          agent any  
           steps {
                  sh 'mvn sonar:sonar -Dsonar.projectKey=AchatProject -Dsonar.host.url=http://172.20.10.5:9000 -Dsonar.login=d23acd12b057dc676f72ab2d4327b0c5fee3fa88'
                  echo 'sonar static analysis done'
           }
         }
         
          
       
    }
}
