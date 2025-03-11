pipeline {
    agent {
        kubernetes {
            defaultContainer 'shell'
            
            yaml """
            apiVersion: v1
            kind: Pod
            spec:
                containers:
                    - name: shell
                      image: ubuntu
                      command: 
                       - sleep
                      args:
                       - infinity
                      hostAliases: 
                       - ip: "172.18.0.50"
                         hostnames:
                          - "gitea.localhost.com"
            """
        }
    }

    stages {
        stage('Test') {
            steps {
                sh 'hostname'
            }
        }
    }
}