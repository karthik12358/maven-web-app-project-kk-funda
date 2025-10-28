pipeline {
    agent any

    tools {
        maven "maven"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'staging', credentialsId: 'homegit-passwd', url: 'https://github.com/karthik12358/maven-web-app-project-kk-funda.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Sonar Analysis') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    echo "Deploying WAR to Tomcat..."
                    curl -u karthik:password \
                    --upload-file target/maven-web-application.war \
                    "http://13.232.108.91:8080/manager/text/deploy?path=/devops144&update=true"
                '''
            }
        }
    }

    post {
        success {
            slackSend channel: '#practice505', 
                      color: 'black', 
                      message: "✅ SUCCESS: Job '${env.JOB_NAME}' #${env.BUILD_NUMBER} completed successfully."
        }

        failure {
            slackSend channel: '#practice505', 
                      color: 'danger', 
                      message: "❌ FAILURE: Job '${env.JOB_NAME}' #${env.BUILD_NUMBER} failed. Check Jenkins for logs."
        }

        unstable {
            slackSend channel: '#practice505',
                      color: 'warning',
                      message: "⚠️ UNSTABLE: Job '${env.JOB_NAME}' #${env.BUILD_NUMBER} had warnings."
        }
    }
}
