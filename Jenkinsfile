node {  
    docker.withRegistry('', '832a713f-d6a0-4a37-99cd-72dff8e0475b') {

        git url: "https://github.com/iconstorage/hello-kubernetes.git", credentialsId: '832a713f-d6a0-4a37-99cd-72dff8e0475b'
        env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
        stage "Build"
        def helloK8s = docker.build "iconstorage/hello-kubernetes"

        stage "Publish"
        helloK8s.push 'latest'
        helloK8s.push "${env.GIT_COMMIT}"

        stage "Deploy"    
      kubernetesDeploy configs: 'hello-kubernetes-dep.yaml', kubeConfig: [path: ''], kubeconfigId: '3a0c84f5-9674-4173-bb09-3bea5a62969b', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
    }
}
