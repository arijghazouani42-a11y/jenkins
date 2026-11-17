pipeline {
    agent any
    options { timestamps() }

    stages {

        stage('Checkout') {
            steps {
                echo '=== Checkout : récupération du code ==='
                git url: 'https://github.com/arijghazouani42-a11y/jenkins.git', branch: 'master'
                bat 'git status'
            }
        }

        stage('Build') {
            steps {
                echo '=== Build : préparation du projet ==='
                bat 'dir'
                bat 'if not exist build mkdir build'
                bat 'copy /Y index.html build'
            }
        }

        stage('Test') {
            steps {
                echo '=== Test : vérification du projet ==='
                bat 'if exist index.html (echo index.html trouvé) else (echo index.html introuvable & exit 1)'
                bat 'findstr /i "<html" index.html'
            }
        }

        stage('Deploy') {
            steps {
                echo '=== Deploy : déploiement local ==='
                bat 'if not exist deploy mkdir deploy'
                bat 'copy /Y build\\index.html deploy'
                bat 'echo Le fichier index.html est déployé dans le dossier deploy'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS : pipeline terminé avec succès'
        }
        failure {
            echo 'FAILURE : le pipeline a échoué, vérifie la Console Output'
        }
    }
}
