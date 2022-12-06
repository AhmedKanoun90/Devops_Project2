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
       
    
       
         stage("SonarQube Analysis") {
          agent any  
           steps {
                  sh 'mvn sonar:sonar -Dsonar.projectKey=AchatProject -Dsonar.host.url=http://172.20.10.5:9000 -Dsonar.login=d23acd12b057dc676f72ab2d4327b0c5fee3fa88'
                  echo 'sonar static analysis done'
           }
         }
         
          
       
    }
}
