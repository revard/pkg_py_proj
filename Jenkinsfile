pipeline {
agent {
    docker {
        image 'python:latest'
    }
}
    stages {

        stage('Build') { 
            steps {
                echo 'Generating distribution archives'
                sh """
                    python3 -m pip install --upgrade build
                    python3 -m build
                """                
            }
        }
        
        stage('Deploy') {
            steps {
            environment {
                TEST_PYPI_CREDS = credentials('test-pypi')
            }                
            echo 'Deploying....'
            echo 'Generating distribution archives'
            sh """            
                python3 -m pip install --upgrade twine
                python3 -m twine upload --repository testpypi dist/* -u%${TEST_PYPI_CREDS_USR}% -p%${TEST_PYPI_CREDS_PWD}%
            """        
            }
        }
    }
}
