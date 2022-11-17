pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage ('clean'){
            steps{
                cleanWs()
            }
        }
    }
}
