pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
         steps {
            powershell 'docker images -a'
            powershell """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """
         }
      }
	 stage('Push Container') {
            steps {
                echo "Workspace is $WORKSPACE"
				dir("$WORKSPACE/azurevote") {
				script {
				docker.withRegistry('https://index.docker.io/','DockerHub','org.jenkinsci.plugins.workflow.cps.CpsClosure2@26fffb19') {
				def image = docker.build('manjuladevi123/jenkins-course:latest')
				image.push()
				    }
				  }
			   }
            }
        }
    }
}
