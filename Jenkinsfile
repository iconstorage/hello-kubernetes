node {
    sh "id"
    sh "echo $PATH"
    sh "docker ps"
    docker.image("node:latest").inside("") {
        sh "npm --version"
    }
}
