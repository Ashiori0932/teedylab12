pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('pmd') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }
        stage('Generate Surefire Report') {
            steps {
                bat 'mvn -DskipTests surefire-report:report'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/site/surefire-report.html', fingerprint: true
                }
            }
        }
        stage('Generate Javadoc') {
            steps {
                bat 'mvn -DskipTests javadoc:jar'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
                }
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

    }
  
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
