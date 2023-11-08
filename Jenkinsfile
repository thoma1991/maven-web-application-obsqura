node
 {
  
  def mavenHome = tool name: "Maven-3.9.2"
  
      echo "GitHub BranhName ${env.BRANCH_NAME}"
      echo "Jenkins Job Number ${env.BUILD_NUMBER}"
      echo "Jenkins Node Name ${env.NODE_NAME}"
  
      echo "Jenkins Home ${env.JENKINS_HOME}"
      echo "Jenkins URL ${env.JENKINS_URL}"
      echo "JOB Name ${env.JOB_NAME}"
  
   // properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '2')), pipelineTriggers([pollSCM('* * * * *')])])
  
  stage("CheckOutCodeGit")
  {
   git 'https://github.com/Sivay3005/maven-web-application-obsqura.git'
   sh "ls"
 }
 
 stage("Build")
 {
 sh "${mavenHome}/bin/mvn clean package"
 }
 
  
 stage("ExecuteSonarQubeReport")
 {
 sh "${mavenHome}/bin/mvn clean package sonar:sonar \
  -Dsonar.projectKey=maven-web-application-obsqura \
  -Dsonar.host.url=http://18.204.10.15:9000 \
  -Dsonar.login=sqp_f06414594231f0e78dd3783544e85c9762b5afea"
 }
 
 stage("UploadArtifactsintoNexus")
 {
 sh "${mavenHome}/bin/mvn deploy"
 }
 
 //  stage("DeployAppTomcat")
 // {
 //  sshagent(['423b5b58-c0a3-42aa-af6e-f0affe1bad0c']) {
 //    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@15.206.91.239:/opt/apache-tomcat-9.0.34/webapps/" 
 //  }
 // }
 
 // stage('EmailNotification')
 // {
 // mail bcc: 'devopstrainingblr@gmail.com', body: '''Build is over

 // Thanks,
 // Mithun Technologies,
 // 9980923226.''', cc: 'devopstrainingblr@gmail.com', from: '', replyTo: '', subject: 'Build is over!!', to: 'devopstrainingblr@gmail.com'
 // }
 // */
 
 }
