pipeline {
    agent {
        kubernetes {
            yaml """
            apiVersion: v1
            kind: Pod
            spec:
                containers:
                    - name: python
                      image: python:3.9.12-alpine3.15
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
        stage('Unit tests') {
            steps {
                container("python") {
                    sh '''
                        pip install -r requirements.txt
                        pytest -v --disable-warnings
                        bandit -r . -x '/tests/'
                        black .
                        flake8 .
                    '''
                }
            }
        }
    }
}