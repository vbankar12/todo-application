node {
    def IMAGE_NAME = "vbankar12/todo-application:latest"

    stage('clone') {
            git 'https://github.com/vbankar12/todo-application.git'
    }
    
    stage('Build'){
         sh 'mvn clean package -DskipTests'
    }

    stage('Docker push'){
        sh "docker tag todo-application-image vbankar12/todo-application:latest"
        sh "docker push vbankar12/todo-application:latest"
    
    } 
    
    stage('Deploye with compose') {
        sh 'docker rm -f mysql-db || true'
        sh 'docker compose down || true'
        sh 'docker compose up -d'
    }   
    
    stage('Cleanp') {
     sh 'rm -rf *'
    }
}     
