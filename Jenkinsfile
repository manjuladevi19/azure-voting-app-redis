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
	 stage('Run Trivy') {
               steps {
                  sleep(time: 30, unit: 'SECONDS')
                   powershell """
                  C:\\Windows\\System32\wsl.exe -- sudo trivy manjuladevi123/jenkins-course
                   """
               }
            }
    }
}
