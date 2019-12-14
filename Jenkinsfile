pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/uttamrao/jenkins-example.git'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'localmaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'localmaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'localmaven') {
                    sh 'mvn install'
                }
            }
        }

         stage ('deploy to tomcat') {
             steps {
                 sshagent(['tomcat']) {
                 sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@172.31.40.139:/var/lib/tomcat/webapps/'
      }
             }
   }
}
}
