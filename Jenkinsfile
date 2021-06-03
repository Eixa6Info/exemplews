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
        stage('Test') {
          agent {
               docker { image 'node:14-alpine' }
          }
          steps {
                sh 'node --version'
            }
        }
   
      stage('Docker') {
       agent {
          docker {image 'docker'}
        }
        steps {
            echo 'Execution de docker'
            sh 'docker -v'
            sh 'docker build -t fabien6668/exemplews .'
          
        }
      }
    }
}
