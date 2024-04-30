pipeline {
    agent any
    stages {
         stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/KartikRohilla10/CI_CD.git'
            }
        }
        stage('Dependencies') {
            steps {
                sh "npm install" // corrected npm spelling
                 // corrected npm spelling and added missing double quotes
            }
        }
        stage('Build') {
            steps {
                // corrected npm spelling
                sh "npm run build" // corrected npm spelling and added missing double quotes
            }
        }
        stage('Test') {
            steps {
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
