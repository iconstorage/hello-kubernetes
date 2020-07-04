node {  
    docker.withRegistry('', 'f1b62afa-a6b3-4030-a168-06f69c6cdb5d') {

        git url: "https://github.com/iconstorage/hello-kubernetes.git", credentialsId: '832a713f-d6a0-4a37-99cd-72dff8e0475b'
        env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
        stage "Build"
        def helloK8s = docker.build "michaelatnutanix/hello-kubernetes"

        stage "Publish"
        helloK8s.push 'latest'
        helloK8s.push "${env.GIT_COMMIT}"

        stage "Deploy"    
      kubernetesDeploy configs: 'hello.yaml', enableConfigSubstitution: true, kubeConfig: [path: ''], kubeconfigId: '3a0c84f5-9674-4173-bb09-3bea5a62969b', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
    }
}
