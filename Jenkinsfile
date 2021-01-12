node {
    docker.withRegistry(credentialsId: 'paulovdt', url: 'https://hub.docker.com/repository/docker/paulovdt/hello-kubernetes') {

        git url: "https://https://github.com/paulovdt55/hello-kubernete", credentialsId: '9dcd2591-9066-4ff9-8c20-f5b09fcc665d'
        env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()

        stage "Build"
        def helloK8s = docker.build "michaelatnutanix/hello-kubernetes"

        stage "Publish"
        helloK8s.push 'latest'
        helloK8s.push "${env.GIT_COMMIT}"

        stage "Deploy"
        kubernetesDeploy configs: 'hello-kubernetes-dep.yaml', kubeConfig: [path: ''], kubeconfigId: 'aa396894-f9df-4e21-b6e2-08737514682c', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']

    }
}
