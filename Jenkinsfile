
node

    {
      def mavenHome=tool name: "mvn123"
      
      stage ('git checkout')
     {

      git branch: 'version2', credentialsId: 'git', url: 'https://github.com/karthik12358/maven-web-app-project-kk-funda.git'


      }
     
      stage ('build stage')
     {
        
       sh  "${mavenHome}/bin/mvn clean package"
     }



      stage ('sonar stage')
     {
        
       sh  "${mavenHome}/bin/mvn clean sonar:sonar" 


       }
   
      stage ('nexus stage')
     {
        
       sh  "${mavenHome}/bin/mvn clean deploy sonar:sonar" 


       }

  
stage('deploy to tomcat') {
    echo "Deploying WAR file using curl..."
    sh """
        curl -u karthik:amma123 --upload-file /var/lib/jenkins/workspace/jio-script/pipeline/target/maven-web-application.war \
        http://13.201.5.127:8080/manager/text/deploy?path=/maven-web-application&update=true
    """
}

  






 }//closing node
