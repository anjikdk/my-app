@Library('ram-libs') _

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
                tomcatDeploy('tomcat-dev','ec2-user','15.206.93.140')
            }
        }
    }
}
