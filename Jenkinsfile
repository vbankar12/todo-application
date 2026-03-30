node {
    def IMAGE_NAME = "vbankar12/todo-application:lates"

    stage('clone') {
            git 'https://github.com/vbankar12/todo-application.git'
    }
    
    stage('Build'){
         sh 'mvn clean package -DskipTests'
    }

    stage('Docker Build') {
         sh 'docker build -t todo-application-image .'
    }
    
    stage('Docker Login'){
        sh 'docker login -u vbankar12 -P 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'
            } 
    }
    stage('Docker push') {
        sh "docker push vbankar12/todo-applicaion:latest"
    }

    stage('Deploye with compose') {
        sh 'docker compose down || true'
        sh 'docker compose up -d'
    }   
    
    stage('Cleanp') {
     sh 'rm -rf *'
    }
     
}