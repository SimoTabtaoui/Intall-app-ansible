
pipeline {

    agent any

    environment {
        DEFAULT_ADMIN_USER = 'admin'
    }

    parameters {
        string(
            name: 'HOST',
            description: 'Hostname ou IP de la machine à configurer')

        password(
            name: 'ADMIN_PASSWORD',
            description: 'Mot de passe du user admin sur la machine HOST.')
    }

    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install App') {
            environment {
                HOST_LIST = "${HOST},"
            }
            steps {
                sh '''
                    export ANSIBLE_HOST_KEY_CHECKING=False
                    ansible-playbook playbook.yml \
                    -i ${HOST_LIST} \
                    -e ansible_user=${DEFAULT_ADMIN_USER} \
                    -e ansible_password=${ADMIN_PASSWORD} \
                    -e ansible_sudo_pass=${ADMIN_PASSWORD} \
                    -vvv
                '''
            }
        }
    }
}
