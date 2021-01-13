// Author : Shailendra V
// Jenkinsfile

pipeline {
   agent any
   tools ('Init') {
      maven "localMaven"
    }
   stages {
      stage('Build') {
		steps {
			git 'https://github.com/shailendravaichalkar/MavenSelenium.git'
		}
      }
      stage('Test and Install') {           
        steps {
			// bat "mvn clean install -Dbrowser=chrome -Dheadless=true"
      bat "mvn clean verify"
        }
      } 
	  stage('Deploy') {
	    steps {
	        //archiveArtifacts 'target/*.jar'
          echo "Deployed"
	    }
      }
	} 
	post {
      always {
        // emailext body: '$DEFAULT_CONTENT', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'JENKINS: (${JOB_NAME}) (${BUILD_NUMBER}) : $DEFAULT_SUBJECT',to: 'vaichalkar.shailendra@gmail.com'
        echo "Mail Sent"
      }
    }
}
