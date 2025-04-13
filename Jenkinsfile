pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
        VENV_DIR = "venv"
    }

    stages {
        stage('Cloner le dépôt') {
            steps {
                git 'https://github.com/Issakha23/myapp.git'
            }
        }

        stage('Créer un environnement virtuel') {
            steps {
                sh 'rn -rf ${VENV_DIR}'
		sh 'python3 -m venv $(VENV_DIR)'
            }
        }

        stage('Installation des dépendances') {
            steps {
                sh "./{VENV_DIR}/bin/pip install --upgrade pip"
                sh "./{VENV_DIR}/pip install -r requirements.txt"
            }
        }

        stage('Tests') {
            steps {
                sh "./${VENV_DIR}/bin/pytest test_app.py"
            }
        }
	stage('Déploiement') {
            steps {
                sh "./${VENV_DIR}/bin/ansible-playbook -i inventory deploy.yml'
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

