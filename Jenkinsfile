pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                git 'https://github.com/Issakha23/myapp.git'
            }
        }

        stage('Installation des dépendances') {
            steps {
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
                sh 'ansible-playbook deploy.yml --ask-vault-pass'
            }
        }
    }

    post {
        failure {
            echo "Le pipeline a échoué !"
        }
        success {
            echo "Pipeline réussi !"
        }
    }
}
