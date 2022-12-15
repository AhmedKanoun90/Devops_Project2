pipeline {
    agent any

    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "172.20.10.5:8081"
        NEXUS_REPOSITORY = "deploymentRepo"
        NEXUS_CREDENTIAL_ID = "nexus1"
    }
    stages {
        stage ('maven clean') {
      steps {
        sh 'mvn clean -e'
        echo 'Build stage done'
      }
    }
   
        stage("compile Project"){
            steps {
                 sh 'mvn compile'
                  echo 'compile stage done'
            }
        }
        stage("maven tests"){
            steps {
                 sh 'mvn test'
                echo 'unit tests stage done'
            }
        }
       
        stage("SonarQube Analysis") {
          
           steps {
            withSonarQubeEnv('sq1') 
            {
                  sh ''' 
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=cidevops 
                        
                        '''
                  echo 'sonar static analysis done'
           }
           }
         }
         
          stage("maven package") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }
       
    stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
    }
   
}
//pipeline {
  //  agent any
    //stages {  
      //  stage("Cloning Project"){
        //    steps {
          //    git branch: 'master',
            //   url: 'https://github.com/riadh70/Devops_Project.git'
              // echo 'checkout stage'
            //}
        //} 
       
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
        
    //   stage("Build") { 
    //     steps {  
     //        sh script: 'mvn clean package' 
     //   } 
  //   }
  //   stage("Upload Jar  To Nexus") {
   //         steps {  
    //             nexusArtifactUploader artifacts: [ 
    //                 [ 
    //                   artifactId: 'tpAchatProject',  
     //                  classifier: '',  
    //                   file: 'target/tpAchatProject-1.0.jar', 
    //                   type: 'jar' 
    //                ]  

    //         ],  
    //         credentialsId: 'nexus1', 
    //         groupId: 'com.esprit.examen', 
     //        nexusUrl: '172.20.10.5:8081', 
     //        nexusVersion: 'nexus3', 
     //        protocol: 'http', 
     //        repository: 'deploymentRepo',  
    //         version: '1.0' 


    //      }  

   //   } 

         
          
       
 //   }
//}
