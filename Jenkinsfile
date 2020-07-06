node {  
    docker.withRegistry('', 'f1b62afa-a6b3-4030-a168-06f69c6cdb5d') {

        git url: "https://github.com/iconstorage/hello-kubernetes.git", credentialsId: '832a713f-d6a0-4a37-99cd-72dff8e0475b'
        env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
        stage "Build"
        def helloK8s = docker.build "iconstorage/hello-kubernetes"

        stage "Publish"
        helloK8s.push 'latest'
        helloK8s.push "${env.GIT_COMMIT}"

        stage "Deploy"    
   kubernetesDeploy configs: 'hello-kubernetes-dep.yaml', kubeConfig: [path: ''],  kubeconfigId: '1d5bd248-480c-4c26-8143-921687e89a62', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
    }
}
