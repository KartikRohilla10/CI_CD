pipeline {
    agent any
    stages {
        stage('Installing Dependencies') {
            steps {
                echo '______________Installing dependencies______________ '
                sh 'npm install'
            }
        }
        stage('Docker Build') {
            steps {
                echo '______________Building Docker image______________'
                sh 'docker build -t reactapp .'
            }
        }
        stage('Docker Login & Push ') {
            steps {
                echo '______________Logging into Docker registry______________'
                withCredentials([usernamePassword(credentialsId: "dockercred", passwordVariable: "dockerPass", usernameVariable: "dockerUser")]) {
                   sh "docker tag reactapp ${env.dockerUser}/reactapp:latest"
                    sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                    sh "docker push ${env.dockerUser}/reactapp:latest"
                }
                
            }
        }
        stage('Build (npm)') {
            steps {
                echo '______________Building React app______________'
                sh 'npm run build'
            }
        }
        stage('Test (npm)') {
            steps {
                echo '______________Testing React apps______________'
                sh 'npm test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                echo '______________SonarQube Analysis______________'
                script {
                    def scannerHome = tool 'sonar-scanner';
                    withSonarQubeEnv() {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        stage('Serve to Nginx') {
            steps {
                echo '______________Copying build files to Nginx directory______________'
                sh 'sudo rm -rf /var/www/react'
                sh 'sudo cp -r ${WORKSPACE}/build/ /var/www/react/'
            }
        }
    }
}
