pipeline {
    agent any

    environment {
        VIRTUAL_ENV = "${WORKSPACE}/venv"
        PATH = "${VIRTUAL_ENV}/bin:${env.PATH}"
    }

    stages {
        stage('Cloner le dépôt') {
            steps {
                git url: 'https://github.com/Issakha23/myapp.git'
            }
        }

        stage('Créer un environnement virtuel') {
            steps {
                sh 'python3 -m venv venv'
            }
        }

        stage('Installation des dépendances') {
            steps {
                sh 'pip install --upgrade pip'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Déploiement') {
            steps {
                sh 'ansible-playbook -i inventory deploy.yml --ask-vault-pass'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline exécuté avec succès !'
        }
        failure {
            echo '❌ Le pipeline a échoué.'
        }
    }
}

