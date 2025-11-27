pipeline {
    agent any
    tools {
        git 'Default'
    }
    stages {
        stage('Prepare Environment') {
                steps {
                    script {
                        bat 'chmod +x ./gradlew'
                    }
                }
            }
        stage('Checkstyle Main') {
            steps {
                script {
                    bat './gradlew checkstyleMain'
                }
            }
        }
        stage('Checkstyle Test') {
            steps {
                script {
                    bat './gradlew checkstyleTest'
                }
            }
        }
        stage('Compile') {
            steps {
                script {
                    bat './gradlew compileJava'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    bat './gradlew test'
                }
            }
        }
        stage('JaCoCo Report') {
            steps {
                script {
                    bat './gradlew jacocoTestReport'
                }
            }
        }
        stage('JaCoCo Verification') {
            steps {
                script {
                    bat './gradlew jacocoTestCoverageVerification'
                }
            }
        }
    }

    post {
        always {
            script {
                def buildInfo = "Build number: ${currentBuild.number}\n" +
                                "Build status: ${currentBuild.currentResult}\n" +
                                "Started at: ${new Date(currentBuild.startTimeInMillis)}\n" +
                                "Duration so far: ${currentBuild.durationString}"
                echo ' Sending telegram message: \n${buildInfo}'
                telegramSend(message: buildInfo)
            }
        }
     }
}
