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
                    hostname
                    pwd
                    ls -l
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
                    hostname
                    pwd
                    ls -l
                    ls -l ./dist                 
                    python3 -m pip install --upgrade twine
                    python3 -m twine upload --repository  ./dist/* -u%username% -p%password%
                """        
            }
        }
    }
}



+ ls -l ./dist

total 8

-rw------- 1 root root 2347 Jul  5 15:44 hello_world-0.0.1-py3-none-any.whl

-rw------- 1 root root 3270 Jul  5 15:44 hello_world-0.0.1.tar.gz

dist/hello_world-0.0.1-py3-none-any.whl