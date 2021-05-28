pipeline {
  agent any
  triggers{ cron('H/5 * * * *') }
  tools { 
        maven 'maven' 
        jdk 'jdk8' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }
        stage('Build') {
             steps {
                echo 'Build'
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
             }
             post {
                success {
                    echo 'Success'
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
    }
}
