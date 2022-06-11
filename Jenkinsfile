node {
    git poll: true, url: 'https://github.com/CSID-DGU/2022-1-OSSPrac-WonheungUnion-7'
    withCredentials([[$class: 'UsernamePasswordMultiBinding',

    credentialsId: 'docker-hub',

    usernameVariable: 'DOCKER_USER_ID', 

    passwordVariable: 'DOCKER_USER_PASSWORD']]) { 
    
        stage('Pull') {
            git clone 'https://github.com/CSID-DGU/2022-1-OSSPrac-WonheungUnion-7'
        }
        stage('Unit Test') {
            
        }
        stage('Build'){
            sh(script: 'docker-compose build')
        }
        stage('Tag') {
            sh(script: '''docker tag ${DOCKER_USER_ID}/uwsgi-nginx-flask \
            ${DOCKER_USER_ID}/uwsgi-nginx-flask:${BUILD_NUMBER}''') 
        }
        stage('Push') {
            sh(script: 'docker login -u ${DOCKER_USER_ID} -p ${DOCKER_USER_PASSWORD}')
            sh(script: 'docker push ${DOCKER_USER_ID}/uwsgi-nginx-flask:${BUILD_NUMBER}') 
            sh(script: 'docker push ${DOCKER_USER_ID}/uwsgi-nginx-flask:latest')
        }
        stage('Deploy') {
            sh(script: 'docker-compose up -d production')
        }
    }
}