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
        stage('Reload Website') {
        steps {
            echo 'Reloading website using BrowserSync'
            sh 'cd /var/www/react && browser-sync start --server --files "*.html, *.css, *.js" --no-open &'
            }
        }
    }
}
