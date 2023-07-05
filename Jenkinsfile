pipeline {
    agent { node { label 'pkgbuild' } }
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
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:writerServerCredId,
                                usernameVariable: 'TWINE_USERNAME', passwordVariable: 'TWINE_PASSWORD']
                ]) {
                    echo 'Generating distribution archives'
                    sh """
                        python3 -m pip install --upgrade twine
                        python3 -m twine upload --repository testpypi dist/*
                    """
                }        
            }
        }
    }
}