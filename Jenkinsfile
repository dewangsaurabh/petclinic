pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh "mvn clean install -DskipTests=true"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Docker build') {
            steps {
                sh "docker build -t dewangsa/petclinic" 
            }
        }
         stage('Docker publish') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_creds', passwordVariable: 'password', usernameVariable: 'user')]) {
                    sh "docker login -u ${user} -p ${password};
                    docker push dewangsa/petclinic "
                }
            }
        }
         stage('Deploy') {
            steps {
               gcloud container clusters get-credentials batmanbegins --zone=us-central1-a
               kubectl apply -f DEV/
 
            }
        }
    }
}
