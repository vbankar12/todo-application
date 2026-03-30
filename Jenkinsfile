
pipline{
    agent any

    envirnoment {
        DOCKER_IMAGE = "vbankar12/todo-application:latest"
    }
    stages('clone') {
        steps {
            git 'https://github.com/vbankar12/todo-application.git'
    
        }
    }
    stage('Build Maven'){
        steps {
            sh 'mvn clean packge -DskipTests'
        }
    }
    stages('Build Docker Image') {
        steps {
            sh 'docker build -t todo-application-image .'
            sh 'docker tag todo-application-image vbankar12/todo-applicaion:latest'
        }
    }
    stage('Push Docker Image'){
        steps{
            withCredentials([usernamePassword(crednetialsId: 'docker-hub-credentials', usernameVariable:'USER', passwordVariable: 'PASS')]) {
                sh 'echo $PASS | docker login -u $USER --password-stdin'
                sh 'docker push vbankar12/todo-applicaion:latest'
            }

         }
    }
    
stage('Deploy') {
    steps {
        sh 'docker-compose down'
        sh 'docker-compose up -d'
    }
}
stage('Cleanup') {
    steps {
        sh 'rm -rf *'
    }
  } 
}