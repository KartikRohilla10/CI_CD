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
        stage('Build') {
            steps {
                echo 'Build React app'
                sh "npm run build" // corrected npm spelling and added missing double quotes
            }
        }
        stage('Test') {
            steps {
                echo 'Testing React app'
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
