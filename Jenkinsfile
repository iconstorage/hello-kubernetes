node {
    docker.withRegistry('', 'e25b0551-7255-4a1f-b6fe-64f5338f96ec') {

        git url: "https://github.com/iconstorage/hello-kubernetes.git", credentialsId: '8c86de93-5329-4ccb-b6f8-fb06ff29e433'
        env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
        stage "Build"
        def helloK8s = docker.build "iconstorage/hello-kubernetes"

        stage "Publish"
        helloK8s.push 'latest'
        helloK8s.push "${env.GIT_COMMIT}"

        stage "Deploy"    
        kubernetesDeploy configs: 'hello-kubernetes-dep.yaml', kubeConfig: [path: ''], kubeconfigId: '83bd2369-aed1-4ebb-8250-37eae5422e9a', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
    }
}
