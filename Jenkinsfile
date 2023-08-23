pipeline {
    agent { label 'dev-agent' }
    stages {
        stage ('Code'){
            steps {
                git url: 'https://github.com/pawarraviraj834/node-todo-cicd.git', branch: 'master'
            }
        }
        stage ('Built and test'){
            steps {
                sh 'docker build . -t pawarraviraj834/node-todo-cicd:latest'
            }
        }
        stage ('Login and push image'){
            steps {
                echo "Pushing image"
                withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD}"
                    sh "docker push pawarraviraj834/node-todo-cicd:latest"
                }
            }
        }
        stage ('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
