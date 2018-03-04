node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "hello-kenzan"
    registryHost = "127.0.0.1:30400/"
    imageName = "${registryHost}${appName}:${tag}"
    env.BUILDIMG=imageName

    stage "Build"
        sh "SET DOCKER_TLS_VERIFY=1"
sh "SET DOCKER_HOST=tcp://192.168.99.102:2376"
sh "SET DOCKER_CERT_PATH=C:\Users\mrhuang\.docker\machine\machines\default"
sh "SET DOCKER_MACHINE_NAME=default"
sh "SET COMPOSE_CONVERT_WINDOWS_PATHS=true"
sh "REM Run this command to configure your shell:"
sh "REM     @FOR /f "tokens=*" %i IN ('docker-machine env --shell cmd default') DO @%i"
        sh "docker build -t ${imageName} -f applications/hello-kenzan/Dockerfile applications/hello-kenzan"
    
    stage "Push"

        sh "docker push ${imageName}"

    stage "Deploy"

        sh "sed 's#127.0.0.1:30400/hello-kenzan:latest#'$BUILDIMG'#' applications/hello-kenzan/k8s/deployment.yaml | kubectl apply -f -"
        sh "kubectl rollout status deployment/hello-kenzan"
}
