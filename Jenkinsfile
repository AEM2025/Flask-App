pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'my-docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh '''
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker build . -t ahmedemad2025/flask-app:v3
                docker push ahmedemad2025/flask-app:v3
                '''
                }
            }
        }
         stage('CD') {
            steps {

                withCredentials([usernamePassword(credentialsId: 'my-docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh '''
		kubectl apply -f /var/jenkins_home/workspace/admin/
                '''
                }
            }
        }
    }
}
