pipeline{
    agent any
    environment{
        DOCKERHUB_CREDENTIALS = credentials("dockerhub")
    }
    stages{
        stage('init'){
            steps{
                sh 'docker rm -f $(docker ps -aq) || true'

             }

        }
        stage("build"){
            steps{
                sh "chmod +x deploy.sh"
                sh "./deploy.sh"
            }
        }
        stage("push"){
            steps{
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"
                sh "docker tag trio-task-mysql:5.7 lewis1401/mytriotaskmysql:latest"
                sh "docker tag trio-task-flask-app lewis1401/mytriotaskflask:latest"
                sh "docker push lewis1401/mytriotaskmysql:latest"
                sh "docker push lewis1401/mytriotaskflask:latest"
            }
        }


    }

}
