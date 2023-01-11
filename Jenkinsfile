pipeline{
    agent any
    
    environment{
        PATH = "/opt/maven3/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
               git branch: 'main', credentialsId: 'b026e5d6-49bc-43f9-9464-6466e138fcb9', url: 'https://github.com/81062/amazondev.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
                sh "mv target/*.war target/myweb.war"
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-new']) {
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war  ubuntu@ec2172.31.42.160:/home/ubuntu/apache-tomcat-8.5.84/webapps/
                    
                    ssh ubuntu@ec2172.31.42.160 /home/ubuntu/apache-tomcat-8.5.84/bin/shutdown.sh
                    
                    ssh ubuntu@ec2172.31.42.160 /home/ubuntu/apache-tomcat-8.5.84/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}