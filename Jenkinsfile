pipeline {
    agent any
    stages {
        stage('Dependencies') {
            steps {
                echo '____________________________________________________________Installing dependencies____________________________________________________________ '
                sh 'npm install'
            }
        }
        stage('Docker Build') {
            steps {
                echo '____________________________________________________________Building Docker image____________________________________________________________'
                sh 'docker build -t reactapp .'
            }
        }
        stage('Docker Login') {
            steps {
                echo '____________________________________________________________Logging into Docker registry____________________________________________________________'
                withCredentials([usernamePassword(credentialsId: "dockercred", passwordVariable: "dockerPass", usernameVariable: "dockerUser")]) {
                    sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                }
            }
        }
        stage('Build') {
            steps {
                echo '____________________________________________________________Building React app____________________________________________________________'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                echo '____________________________________________________________Testing React apps____________________________________________________________'
                sh 'npm test'
            }
        }
        stage('____________________________________________________________Serve to Nginx____________________________________________________________') {
            steps {
                echo 'Copying build files to Nginx directory'
                sh 'sudo rm -rf /var/www/react'
                sh 'sudo cp -r ${WORKSPACE}/build/ /var/www/react/'
            }
        }
    }
}
