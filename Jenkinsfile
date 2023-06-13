pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'my-docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh '''
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker build . -t ahmedemad2025/flask-app:v$BUILD_NUMBER
                docker push ahmedemad2025/flask-app:v$BUILD_NUMBER
                '''
                }
            }
        }
         stage('CD') {
            steps {

                withCredentials([usernamePassword(credentialsId: 'my-docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh '''
		sed -i 's/mytag/${BUILD_NUMBER}/g' deployment.yml
		kubectl apply -f deployment.yml
                '''
                }
            }
        }
    }
}
