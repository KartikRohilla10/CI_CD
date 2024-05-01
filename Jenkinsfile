pipeline {
    agent any
    stages {
        stage('Dependencies') {
            steps {
                echo '________Installing dependencies________ '
                sh 'npm install'
            }
        }
        stage('Docker Build') {
            steps {
                echo '________Building Docker image________'
                sh 'docker build -t reactapp .'
            }
        }
        stage('Docker Login') {
            steps {
                echo '________Logging into Docker registry________'
                withCredentials([usernamePassword(credentialsId: "dockercred", passwordVariable: "dockerPass", usernameVariable: "dockerUser")]) {
                   sh "docker tag reactapp ${env.dockerUser}/reactapp:latest"
                    sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                    sh "docker push ${env.dockerUser}/reactapp:latest"
                }
                
            }
        }
        stage('Build') {
            steps {
                echo '________Building React app________'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                echo '________Testing React apps________'
                sh 'npm test'
            }
        }
        stage('Serve to Nginx') {
            steps {
                echo '________Copying build files to Nginx directory________'
                sh 'sudo rm -rf /var/www/react'
                sh 'sudo cp -r ${WORKSPACE}/build/ /var/www/react/'
            }
        }
    }
}
