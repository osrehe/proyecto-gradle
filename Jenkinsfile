pipeline {
    agent any

    stages {
        stage('INFO'){
            steps{
                echo 'Info...'
                //slackSend color: "warning", message: "INFO: Prueba Taller 3 - Modulo 4 Branch: ${GIT_BRANCH}"
            }
            post {
                success {
                    echo 'INFO Success'
                    //slackSend color: "good", message: "Info Success. commit ${GIT_COMMIT}"
                }
                failure {
                    echo 'INFO Failed'
                    //slackSend color: "danger", message: "Info Failed."
                }
            }
        }
        stage('SONARQube'){
            steps{
                echo 'Sonar...'
                withSonarQubeEnv('Sonita') {
                    echo "$WORKSPACE" 
                    sh 'chmod -R 755 $WORKSPACE'
                    sh './gradlew sonarqube -Dsonar.projectKey=RemoteGradle --stacktrace --scan'
                }
            }
            post {
                success {
                    echo 'SONAR Success' 
                    //
                }
                failure {
                    echo 'SONAR Failed'
                    //slackSend color: "danger", message: "Sonar Failed."
                }
            }
        }
    }
}