pipeline {

    agent { label 'centos7' }
    stages {
        stage('Clone repository') { 
            steps { 
                    git url:'git@github.com:Dmitry-Shevtsov/drupal_project.git',
                    credentialsId: 'Jenkins_GIT'
            }
        }

        stage('Checks Docker-compose file') {
            steps {
                sh '''
                    docker-compose config
                '''
            }
        }
        
        stage('UP with Docker-compose') {
            steps {
                sh '''
                    docker-compose up -d
                '''
            }
        }

        stage("Wait prior starting testing") {
            steps {
                sleep(time:15,unit:"SECONDS")
            }
        }    

        stage('Checking start page') {
            steps {
                sh '''
                    lynx -dump http://drupal.docker.localhost:8000
                '''
            }
        }
        
        stage('Stopping Docker containers') {
            steps {
                sh 'docker ps -q | xargs --no-run-if-empty docker container stop'
            }
        }

        stage('Removing Docker images') {
          steps{
            sh 'docker container ls -a -q | xargs -r docker container rm'
          }
        }
    }

    post {
            success {
                slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            }
            failure {
                slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            }
        }
}
