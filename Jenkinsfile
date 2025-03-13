node 
   {
      def mavenHome=tool name: "mvn123"    

     stage ('checkout stage1')
    {
  
   git branch: 'test2', credentialsId: '439a99fd-f1f1-4b29-ab8c-fdeb387f9153', url: 'https://github.com/karthik12358/maven-web-app-project-kk-funda.git'

   }


     stage  ('build stage2')
   {
     
     sh  "${mavenHome}/bin/mvn clean package"

  }
 
  stage  ('sonarqube stage3')
 {
    sh  "${mavenHome}/bin/mvn clean sonar:sonar"
 
 }

 stage   ('nexus stage4')

{
 
  sh  "${mavenHome}/bin/mvn clean deploy sonar:sonar"

}

stage  ('deploy tomcat stage5')
{
 echo "Deploying WAR file using curl..."
 
 sh """
        curl -u karthik:amma123 --upload-file /var/lib/jenkins/workspace/freshpipeline/target/maven-web-application.war \
        http://13.235.49.91:8080/manager/text/deploy?path=/maven-web-application.war-v2&update=true
    """
}



}//node closing
