pipeline {
    agent any

    stages {
        stage("Do") {
            steps {
                script {
                    sh "ls ${WORKSPACE}"
                    sh "echo 123"
                }
            }
        }
        stage("Done") {
            steps {
                script {
                    sh "echo 456"
                }
            }
        }
    }
}