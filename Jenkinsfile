pipeline {
    agent any
    stages {
        stage('Dependencies') {
            steps {
                echo 'Installing dependencies '
                sh "npm install" // corrected npm spelling
                 // corrected npm spelling and added missing double quotes
            }
        }
        stage('docker image') {
            steps {
                echo 'Build docker image '
                sh "docker build -t reactapp" // corrected npm spelling
                 // corrected npm spelling and added missing double quotes
            }
        }
         stage('Docker login ') {
            steps {
                echo 'Build Docker image'
                withCredentials([usernamePassword(credentialsId:"dockercred",passwordVariable:"dockerPass",usernameVariable:"dockerUser")]){
                sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}" 
            }
        }
        stage('Build') {
            steps {
                echo 'Build React app'
                sh "npm run build" // corrected npm spelling and added missing double quotes
            }
        }
        stage('Test') {
            steps {
                echo 'Testing React apps'
                sh "npm test" // corrected npm spelling
                
            }
        }
        stage('Serve to Nginx') { // corrected stage name spelling
            steps {
                sh "sudo rm -rf /var/www/react" // corrected rm command
                sh "sudo cp -r ${WORKSPACE}/build/ /var/www/react/" // corrected cp command

                
            }
        }
    }
}
