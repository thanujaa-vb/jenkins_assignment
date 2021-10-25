node{
    def app
    stage('clone repo'){
    checkout scm
    }
    stage('push image'){
    docker.withRegistry('https://registry.hub.docker.com', 'dockerHub'){
        def customImage= docker.build("dockerhub/dockerwebapp")
        customImage.push()
    }
    }
}