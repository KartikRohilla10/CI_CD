pipeline {
    agent any
    stages {
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
        stage('Deploy') { // corrected stage name spelling
            steps {
                sh "sudo rm -rf /var/www/react" // corrected rm command
                sh "sudo cp -r ${WORKSPACE}/build/ /var/www/react/" // corrected cp command

                
            }
        }
    }
}
