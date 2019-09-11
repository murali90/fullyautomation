pipeline{
    agent any 
    

    parameters {
     string(name: 'tomcat_dev', defaultValue: '13.233.85.78', description: 'aws tomcat Staging Server')
         string(name: 'tomcat_prod', defaultValue: '13.233.114.195', description: 'aws  tomcat Production Server')
         stages{
             stage('git checkout'){
              steps {
             checkout([$class: 'GitSCM', 
              branches: [[name: '*/master']], 
               doGenerateSubmoduleConfigurations: false, 
               extensions: [], 
               submoduleCfg: [], 
                userRemoteConfigs: [[url: 'https://github.com/murali90/maven-project.git']]])
         }
             }

         stage('buid'){
              steps{
                  sh 'mvn clean package'
         }
         post{
              success{
                  echo 'archiving artifact'
             archiveArtifacts artifacts: 'webapp/**target/*.war'
              }
         }
         stage('Deploy to stage'){
             steps{
                  sh "scp -i /c/Users/nagamurallidhar/Desktop/keypairs/jenkinsserver.pem **/target/*.war ec2-user@${params.tomcat_dev}:/opt/tomcat-8.5.45/webapps"
         
             }
         }
        
        } 
    }

}
