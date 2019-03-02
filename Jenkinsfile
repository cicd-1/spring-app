@Library(pipeline-library-demo)_

def write( String name){
   echo "hello: $name"
   writeFile file: "/tmp/a.txt", text: "This file is useful, need to archive it. $name"
}
node {
   def mvnHome

   stage("ref lib"){
    write "quickfix"  
   }
   stage("sharedlib"){
    sayHello "test"  
   }
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
}
