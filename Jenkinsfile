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
      stage('Test') {           
        steps {
          parallel(
            Firefox: {
              bat "mvn install -Dbrowser=firefox -Dheadless=false"
            },
            Opera: {
              bat "mvn install -Dbrowser=chrome -Dheadless=false"
            }
          )
        }
      } 
	  stage('Deploy in CERT') {
	    steps {
	        archiveArtifacts 'target/*.jar'
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
