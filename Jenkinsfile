pipeline {   
    agent any  
    environment{     
        dockerImage=""     
        registry="thanu123456/build-image"   
        registryCredential = "dockerHub"  
        }   
        stages {    
            stage('test') {   
                steps {          
                   checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/thanujaa-vb/ci_cd-pipeline.git']]])      
                    }    
                    }    
                    stage("build Docker image/push"){     
                        steps{              
                            script{         
                                dockerImage = docker.build registry  
                                docker.withRegistry( '', registryCredential ) { 
                                                dockerImage.push()  
                                }         
                                }
                                }
                    }
                               stage('deploy') {  
                                       steps { 
                                            script {      
                                              bat 'docker ps -f name=jenkinsContainer '        
                                              bat 'docker container ls -a -fname=jenkinsContainer'  
                                                dockerImage.run("-p 4000:3000 --rm --name jenkinsContainer") 
                                                        } 
                                             }       
                               }
        }
}
