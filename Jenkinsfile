pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Clone'){
            
            steps{
                
                script{
                    
                    git branch: 'main', credentialsId: 'git-credentials', url: 'https://github.com/srikanthgppk007/JENKINS-SONARQUBE-NEXUS.git'
                }
            }
        }
    stage('Maven Build'){
        
        steps{
            
            script{
                def mavenHome = tool name: "maven-3.9.0", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} clean package"
            }
        }
      }
    stage('SonarQube analysis'){
        
        steps{
                script{
                     withSonarQubeEnv(credentialsId: 'sonar-token') {
                     def mavenHome = tool name: "maven-3.9.0", type: "maven"
                     def mavenCMD = "${mavenHome}/bin/mvn"
                     sh "${mavenCMD} sonar:sonar"
                    } 
                }
           }
    }
       stage('upload war to nexus'){ 
           
           steps{
                script{
                    
                   nexusArtifactUploader artifacts: [
                       [
                           artifactId: 'srikanth', 
                           classifier: '', 
                           file: 'target/srikanth-4.05.jar', 
                           type: 'jar'
                           ]
                           ], 
                           credentialsId: 'nexus-credentials', 
                           groupId: 'com', 
                           nexusUrl: '13.233.118.93:8081/', 
                           nexusVersion: 'nexus3', 
                           protocol: 'http', 
                           repository: 'srikanth-repo'
                           version: '4.05
               } 
           }
        }
        
    }
}
