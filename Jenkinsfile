node {  
    docker.withRegistry('', 'ecb731f4-bb25-4c99-b3ca-4b58b8108a90') {

        git url: "https://github.com/iconstorage/hello-kubernetes.git", credentialsId: '97d6d0ed-e45d-44e2-a87d-4385b84e084f'
        env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
        stage "Build"
        def helloK8s = docker.build "iconstorage/hello-kubernetes"

        stage "Publish"
        helloK8s.push 'latest'
        helloK8s.push "${env.GIT_COMMIT}"

        stage "Deploy"    
    kubernetesDeploy configs: 'hello-kubernetes-dep.yaml',  enableConfigSubstitution: false, kubeConfig: [path: ''], kubeconfigId: '1428240f-ca6f-4e65-a857-ce051e2a9bd2', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
    }
}
