pipeline{
    agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage("Build the code with help of maven"){
            steps{
                sh 'mvn clean package'
            }
        }
        stage("Deploy artifact into tomcat"){
            steps{
                sshagent(['tomcat-dev']) {
                    // rename the war file
                    sh "mv target/*.war target/myweb.war"
                    // copy war file from jenkins to tomcat webapps folder
                    sh "scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@15.206.93.140:/opt/tomcat8/webapps"
                    // stop and start tomcat
                    sh "ssh ec2-user@15.206.93.140 /opt/tomcat8/bin/shutdown.sh"
                    sh "ssh ec2-user@15.206.93.140 /opt/tomcat8/bin/startup.sh"
                }
            }
        }
    }
}
