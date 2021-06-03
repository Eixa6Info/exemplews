pipeline {
  agent any
 
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
      stage('Docker') {
        agent {
          docker {image 'docker'}
        }
        steps {
          script {
            sh 'docker -v'
            docker.build('fabien6668/exemplews')
          }
        }
      }
    }
}
