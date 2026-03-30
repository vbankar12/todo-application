node {
    def IMAGE_NAME = "vbankar12/todo-application:lates"

    stages('clone') {
        steps {
            git 'https://github.com/vbankar12/todo-application.git'
        }
    }
    stage('Build'){
        steps {
            sh 'mvn clean packge -DskipTests'
        }
    }
    stages('Docker Build') {
        steps {
            sh 'docker build -t todo-application-image .'
        }
    }
    stage('Docker Login'){
        steps{
            withCredentials([usernamePassword(crednetialsId: 'docker-hub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                sh 'echo $PASS | docker login -u $USER --password-stdin'
            }

         }
    }
    stage('Docker push') {
    steps {
        sh "docker push vbankar12/todo-applicaion:latest"
         }
    }
    stage('Deploye with compose') {
    steps {
        sh 'docker compose down || true'
        sh 'docker compose up -d'
        }   
    }
    stage('Cleanp') {
    steps {
        sh 'rm -rf *'
        }
    } 
}