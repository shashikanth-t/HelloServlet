pipeline {
    agent any
   environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage('Git_Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git_credentials', url: 'https://github.com/shashikanth-t/HelloServlet.git'
                echo 'Code Checkout done sucessfully.'
            }
			}
            stage('CodeBuild ') {
            steps {
            sh 'mvn clean install'
            echo 'Code build done sucessfully.'
            }
            }
            stage('CodeDeploy') {
            steps {
          sshagent(['deploy_user']) {
               
               sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/PJOB-1/target/helloworld.war  ec2-user@3.135.203.165:/opt/apache-tomcat-9.0.98/webapps"
    
                            }         
            }
            }            
        }
    }
