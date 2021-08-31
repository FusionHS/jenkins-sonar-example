pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('dependency-check') {
            steps {
                sh 'mvn dependency-check:check'

            }
        }
        stage('Sonar') {
            steps {
                withSonarQubeEnv('sonar') {
                  sh 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
            always {
                dependencyCheckPublisher pattern: 'build/reports/dependency-check-report.xml'
            }
        }
}
