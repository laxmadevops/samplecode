pipeline{
        agent any
	 environment { 
  CRED = credentials('Forgot@1993') 
 }
        stages{
              stage('Quality Gate Statuc Check'){
                  steps{
                      script{
                      withSonarQubeEnv('sonarqube') { 
                      sh "/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/jenkins-maven/bin/mvn sonar:sonar"
                       }
                      timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
		    sh "/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/jenkins-maven/bin/mvn clean install"
                  }
                }  
              }
            
        }
}
