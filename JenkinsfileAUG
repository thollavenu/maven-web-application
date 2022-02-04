node{
     def mavenhome = tool name: "maven 3.6.2"
    

stage('checkoutcode'){
	git branch: 'development', credentialsId: '4edb052a-5e39-47f5-b9ee-0fd3832282f8', url: 
	'https://github.com/thollavenu/maven-web-application.git'
}
stage('build'){
    
   
    sh "${mavenhome}/bin/mvn clean package"
}
stage('ExecutionSonarQubeReport'){
sh "${mavenhome}/bin/mvn clean sonar:sonar"

}
stage('UploadArtifactsIntoNexus'){
sh "${mavenhome}/bin/mvn clean deploy"
}
stage ('DeploytheAppIntoTomact'){

sshagent(['a2afc3f1-abf4-4727-bbb8-b7820b58dc0c']){
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.169.63:/opt/apache-tomcat-9.0.58/webapps"

}
}
/*stage('sendEmailNotification')
{
mail bcc: 'tholla.venu@gmail.com', body: '''build is completed.!!!!

Regards,
Venugopal
Devops Engineer ''', cc: 'tholla.venu@gmail.com', from: '', replyTo: '', subject: 'Build Completed', to: 'tholla.venu@gmail.com'

}*/

}
