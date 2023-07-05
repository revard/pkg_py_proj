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
                echo 'Deploying....'
                echo 'Generating distribution archives'
                sh """            
                    python3 -m pip install --upgrade twine
                    python3 -m twine upload --repository testpypi dist/* -u%username% -p%password%
                """        
            }
        }
    }
}
