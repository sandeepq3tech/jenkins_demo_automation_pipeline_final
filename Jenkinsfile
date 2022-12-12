pipeline {
    agent any
     tools {
        maven 'Maven'
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                 bat "mvn --version"
            }
            
        }
        stage("Build"){
            steps{
               // bat "mvn package"
                
                echo "build step"
                
            }
            
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcatserver', path: '', url: 'http://13.232.2.189:8080')], contextPath: '/app', war: '**/*.war'        
            }
            
        }
        stage("Deploy on Prod"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcatserver', path: '', url: 'http://3.110.161.127:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
             slackSend channel: 'youtubejenkins', message: 'Success'
        }
        failure{
            echo "========pipeline execution failed========"
             slackSend channel: 'youtubejenkins', message: 'Job Failed'
        }
    }
}
