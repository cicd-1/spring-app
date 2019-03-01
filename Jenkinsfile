node {
   def mvnHome
   stage('Preparation') { 
      git 'https://github.com/cicd-1/spring-app.git'
             
      mvnHome = tool 'maven-3.6.0'
   }
   stage('Build') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
   stage('Results') {
       if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' sonar:sonar -Dsonar.host.url=http://ec2-18-222-40-7.us-east-2.compute.amazonaws.com:9000/"
      } else {
         bat(/"${mvnHome}\bin\mvn" sonar:sonar/)
      }
   }
}
