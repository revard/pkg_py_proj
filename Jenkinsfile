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
                    rm -rf ./dist
                    python3 -m build
                """                
            }
        }
        
        stage('Deploy') {
            environment {
                TEST_PYPI_CREDS = credentials('test-pypi')
            }               
            steps {          
            echo 'Deploying....'
            echo 'Generating distribution archives'
            sh """            
                python3 -m pip install --upgrade twine
                python3 -m twine upload --repository testpypi dist/* -u ${TEST_PYPI_CREDS_USR} -p ${TEST_PYPI_CREDS_PSW}
            """        
            }
        }
    }
}
