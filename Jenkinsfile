
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
       
       stage ('MVN clean') {
         steps {
            sh 'mvn clean -e'
            echo 'Build stage done'
        }
     }
   
      stage("compile Project"){
           steps {
                 sh 'mvn compile -X -e'
                  echo 'compile stage done'
            }
      }
      //  stage("unit tests"){
        //    steps {
           //      sh 'mvn test'
         //         echo 'unit tests stage done'
        //    }
     //   }
         stage("mvn Pckage") {
            steps {
                script {
                   sh "mvn package -DskipTests=true"
               }
            }
        }
      //   stage("SonarQube Analysis") {
      //     steps {
      //         withSonarQubeEnv('sq1') {
      //            sh 'mvn sonar:sonar'
      //         }
                 
      //     }
      //   } 
        
    //   stage("Build") { 
    //     steps {  
     //        sh script: 'mvn clean package' 
     //   } 
  //   }
 //    stage("Upload Jar  To Nexus") {
 //           steps {  
 //                nexusArtifactUploader artifacts: [ 
 //                 [ 
 //                     artifactId: 'tpAchatProject',  
 //                     classifier: '',  
 //                     file: 'target/tpAchatProject-1.0.jar',  
                     // file: '/var/lib/jenkins/workspace/Declerative_pipeline/target/tpAchatProject-1.0.jar', 
 //                     type: 'jar' 
 //                  ]  

 //           ],  
 //            credentialsId: 'nexus3', 
 //            groupId: 'com.esprit.examen', 
 //            nexusUrl: '172.20.10.5:8081', 
 //            nexusVersion: 'nexus3', 
 //            protocol: 'http', 
 //            repository: 'deploymentRepo',  
 //            version: '1.0' 


 //        }  

 //     } 

        stage("Nexus Deploy") {
            steps {
                script {
                    sh "mvn clean package deploy:deploy-file -DgroupId=com.esprit.examen -DartifactId=tpAchatProject -Dversion=1.0 -DgeneratePom=true -Dpackaging=jar -DrepositoryId=deploymentRepo -Durl=http://172.20.10.5:8081/repository/maven-releases/ -Dfile=target/tpAchatProject-1.0.jar"
                }
            }
        }         
          
       
   }
}
