pipeline {
    agent {
        kubernetes {
            yamlFile "JenkinsAgent.yaml"
        }
    }

    stages {
        stage('Unit tests') {
            steps {
                container("python") {
                    sh '''
                        pip install -r requirements.txt
                        pytest -v --disable-warnings
                        bandit -r . -x '/.venv/','/tests/'
                        black .
                        flake8 . --exclude .venv
                    '''
                }
            } 
            when {
                anyOf {
                    branch pattern:  "feature*"
                    branch pattern:  "developer*"
                    branch pattern:  "hotfix*"
                    branch pattern:  "fix*"
                }
            }
        }
    }
}