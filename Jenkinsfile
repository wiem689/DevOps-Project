pipeline { 

    environment { 

        registry = "wiemchalouati/imagedoc" 

        registryCredential = 'wiemid' 

        dockerImage = '' 

    }

    agent any 
   

    stages { 
       

         stage( 'Checkout  GIT' ){
                       steps{
                          echo 'Pulling ... ';
                               git branch:  'main' ,
                              url :'https://github.com/wiem689/ProjetDevops'
                              }
                    }

           stage("Test,Build"){
               steps{

                   bat "mvn clean install"
                    }

                  }

              stage("package"){
               steps{

                   bat "mvn package"
                    }

                  }
                  
               stage("Sonar"){
               steps{

                   bat "mvn sonar:sonar"
                    }

                  }
                  
                stage("Nexus"){
               steps{

                   bat "mvn deploy"
                    }

                  }
           
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        

      

        stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }

        stage('Deploy our image') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                    }

                } 

            }

        } 
       stage('Cleaning up') { 

            steps { 

                bat "docker rmi $registry:$BUILD_NUMBER" 

            }
        } 
       
    }

}
