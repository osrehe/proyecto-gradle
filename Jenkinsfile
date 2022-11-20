def responseStatus = ''

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
        stage('BUILD'){
            steps{
                echo 'Building...'
                sh './gradlew build'
            }
            post {
                success {
                    echo 'Build Success'
                    //slackSend color: "good", message: "Build Success"
                }
                failure {
                    echo 'Build Failed'
                    //slackSend color: "danger", message: "Build Failed"
                }
            }
        }
        stage('RUN'){
            steps{
                echo 'Running...'
                sh './gradlew bootRun&'
                //sh 'curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing'
                sh 'curl -I GET http://localhost:8081/rest/mscovid/test?msg=testing > response.txt'
                //${responseStatus}
                sh(script: 'cat response.txt | grep HTTP/1.1 | cut -d " " -f2', returnStdout: true).trim()
            }
            post {
                success {
                    echo 'Running Success'
                    //slackSend color: "good", message: "Build Success"
                }
                failure {
                    echo 'Running Failed'
                    //slackSend color: "danger", message: "Build Failed"
                }
            }
        }
    }
}