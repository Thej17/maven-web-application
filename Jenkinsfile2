pipeline {
   agent any /*'prod node'*/

   stages {
      stage('checkout'){
         steps {
            git credentialsId: '37b0305a-cf7c-4484-bf75-6001986b54b0', url: 'https://github.com/Thej17/maven-web-application.git'
         }
      }
      stage('build'){
         steps {
          sh "/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven3.3.3/bin/mvn clean package"         }
      }
      stage('sonarQube Analysis'){
          steps {
            sh "/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven3.3.3/bin/mvn sonar:sonar"         }  
      }
      stage('nexus') {
          steps {
              sh "/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven3.3.3/bin/mvn clean deploy"
          }
      }
      stage('DeployAppIntoTomcat'){
          steps {
              sh "cp -r /var/lib/jenkins/workspace/newpipeline/target/*.war /opt/apache-tomcat-8.5.50/webapps/"
          }
      }
   }
              
   }
