pipeline {
    agent {
        kubernetes {
            yaml 
            '''
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
                          - "gitea.localhost.com
            '''
            defaultContainer 'shell'
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