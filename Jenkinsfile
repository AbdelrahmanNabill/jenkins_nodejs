pipeline {
    agent {label 'aws'}

    stages {
        stage('ci') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'Docker_pass', usernameVariable: 'Docker_username')]) {
                sh "docker build -t abdelrahmannabil95/nodejs-project ."
                sh "docker login -u ${Docker_username} -p ${Docker_pass}"
                sh "docker push abdelrahmannabil95/nodejs-project"
            }
            }
        }
        
        
                stage('cd') {
            steps {
                                   withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'Docker_pass', usernameVariable: 'Docker_username')]) {

                git 'https://github.com/AbdelrahmanNabill/jenkins_nodejs'
                sh "docker login -u ${Docker_username} -p ${Docker_pass}"
                sh "docker run --env-file env.list -p 3000:3000 -d abdelrahmannabil95/nodejs-project"
                
            }
            }
        }
        
        
            
        }
    }
