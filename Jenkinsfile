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
                cycletimeStartEvent env, currentBuild
                sh 'mvn -B -DskipTests clean package' 
                cycletimeEndEvent env, currentBuild
            }
        }
        stage('Test') {
            steps {
                cycletimeStartEvent env, currentBuild
                sh 'mvn test'
                cycletimeEndEvent env, currentBuild
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                cycletimeStartEvent env, currentBuild
                sh './jenkins/scripts/deliver.sh'
                cycletimeEndEvent env, currentBuild
            }
        }
    }
}
