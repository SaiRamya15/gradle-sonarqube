pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/SaiRamya15/gradle-sonarqube.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo "Building the project with Gradle"
                bat './gradlew.bat clean build'  // Use 'sh' instead of 'bat' on Linux agents
            }
        }

      stage('Run Jar') {
            steps {
                bat 'java -jar build\\libs\\gradle-githubactions-demo-1.0-SNAPSHOT-17.0.5.jar'
    }
      }
    stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
     stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('sonarQube') {
                        bat "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
    }
}
}

