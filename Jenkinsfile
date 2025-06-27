pipeline {

  agent { label "jenkins-agent" }
         tools{
           jdk 'Java17'
           maven 'Maven3'
         }
         stages {
           stage("Cleanup Workspace"){
             steps {
               cleanWs()
             }
             
           }
           stage("Checkout from SCM") {
             steps{
                 //git branch: 'main', credentialsId: 'github', url: 'https://github.com/massa96/ziama-jenkins.git'
                 git url: 'https://github.com/massa96/ziama-jenkins.git' , branch: 'main', credentialsId: 'github'
             }
           }
           
           stage("Build"){
             steps{
               sh "mvn clean package"
             }
           }
           stage("Test"){
            steps{
              sh "mvn test"
            }
           }
           stage("Sonarqube Scanner"){
             steps{
              script {
                  withSonarQubeEnv(credentialsId: "jenkins-sonar-token"){
                    sh "mvn sonar:sonar"
                  }
              }
             }

           }
           
      }
}
