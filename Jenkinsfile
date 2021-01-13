// Author : Shailendra V
// Jenkinsfile

pipeline {
   agent any
   tools ('Init') {
      maven "localMaven"
    }
   stages {
      stage('Pull Sourse Code') {
		steps {
			git 'https://github.com/shailendravaichalkar/MavenSelenium.git'
		}
      }
      stage('test') {           
        steps {
          parallel(
            Firefox: {
              bat "mvn clean test -Dbrowser=firefox -Dheadless=false"
            },
            IE: {
              bat "mvn clean test -Dbrowser=ie -Dheadless=false"
            },
            Opera: {
              bat "mvn clean test -Dbrowser=opera -Dheadless=false"
            },
            Edge: {
              bat "mvn clean test -Dbrowser=edge -Dheadless=false"
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
