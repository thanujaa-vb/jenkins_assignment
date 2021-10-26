pipeline {   
    agent any  
    environment{     
        dockerImage=""     
        registry="thanu123456/jenkinsimage"   
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
                                              bat 'docker ps -f name=jenkinsImageContainer '        
                                              bat 'docker container ls -a -fname=jenkinsImageContainer'     
                                             }       
                                        }       
                                stage('Docker Run') { 
                                       steps{           
                                              script {     
                                                     dockerImage.run("-p 3000:3000 --rm --name jenkinsImageContainer") 
                                                        }     
                                                    }     
                                           }   
        }
}
