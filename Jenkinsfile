pipeline {
    /* Utilise une image Docker Maven prête à l’emploi */
    agent any
    tools {
        maven 'Maven3'
    }
    /* Étapes principales du pipeline */
    stages {

        stage('Checkout') {
            steps {
                echo ' Clonage du dépôt GitHub...'
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                echo ' Compilation et exécution des tests Maven...'
                sh 'mvn -B clean test'
            }
        }

        stage('Results') {
            steps {
                echo ' Publication des résultats de test...'
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }

    /* Bloc post : notifications et statut final */
    post {
        success {
            echo ' Build terminé avec succès !'
        }
        failure {
            echo ' Échec du build ou des tests.'
        }
        always {
            echo ' Fin du pipeline Jenkins.'
        }
    }
}
