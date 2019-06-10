pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                cycletimeStartEvent this
                sh 'mvn -B -DskipTests clean package' 
                cycletimeEndEvent this
            }
        }
        stage('Test') {
            steps {
                cycletimeStartEvent this
                sh 'mvn test'
                cycletimeEndEvent this
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                cycletimeStartEvent this
                sh './jenkins/scripts/deliver.sh'
                cycletimeEndEvent this
            }
        }
    }
}
