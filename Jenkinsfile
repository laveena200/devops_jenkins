node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/shekharshamra/jenkin.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'mvn'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean install"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'in28minutes-web-servlet-jsp/target/*.war'
   }
   stage('Deployment') {
      sh 'scp -r /root/.jenkins/workspace/fistpipleline/in28minutes-web-servlet-jsp/target/*.war root@10.0.0.5:/opt/apache-tomcat-8.5.50/webapps/'
   }
   }
