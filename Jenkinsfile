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
       
       // stage ('MVN clean') {
     // steps {
       // sh 'mvn clean -e'
       // echo 'Build stage done'
     // }
    //}
   
     //  stage("compile Project"){
        //    steps {
         //        sh 'mvn compile -X -e'
         //         echo 'compile stage done'
         //   }
       // }
      //  stage("unit tests"){
        //    steps {
           //      sh 'mvn test'
         //         echo 'unit tests stage done'
        //    }
     //   }
     //    stage("mvn Pckage") {
      //      steps {
      //          script {
       //             sh "mvn package -DskipTests=true"
        //        }
       //     }
      //  }
      //   stage("SonarQube Analysis") {
      //     steps {
      //         withSonarQubeEnv('sq1') {
      //            sh 'mvn sonar:sonar'
      //         }
                 
      //     }
      //   } 
        
            stage ('Publish to Nexus') {
            nexusPublisher nexusInstanceId: 'DevopsNexus ', nexusRepositoryId: 'DevopsNexus', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: './target/tpAchatProject-1.0.jar']],mavenCoordinate: [artifactId: 'tpAchatProject', groupId: 'com.esprit.examen', packaging: 'jar', version: '1']]]
        } 
         
          
       
    }
}
