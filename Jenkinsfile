pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/aaron-cedillo/CD-Actividad.git'
    }

    stages {
        stage('Clonar Repositorio') {
            steps {
                git REPO_URL
            }
        }

        stage('Verificar Archivos') {
            steps {
                script {
                    if (!fileExists('HTML/index.html') || !fileExists('CSS/styles.css')) {
                        error "Archivos HTML o CSS no encontrados."
                    }
                }
            }
        }

        stage('Despliegue en Preproducción') {
            steps {
                echo 'Desplegando en el entorno de Preproducción...'
            }
        }

        stage('Pruebas Automatizadas') {
            steps {
                script {
                    echo 'Ejecutando pruebas automatizadas...'
                    bat 'curl -I http://127.0.0.1:5500/HTML/index.html || exit 1'
                }
            }
        }

        stage('Despliegue en Producción') {
            steps {
                echo 'Desplegando en el entorno de Producción...'
                // Copia los archivos al directorio de producción en Windows
                bat 'copy HTML\\index.html C:\\ruta\\de\\produccion\\'
                bat 'copy CSS\\styles.css C:\\ruta\\de\\produccion\\'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completado.'
        }
        success {
            echo 'El pipeline se ejecutó correctamente y el despliegue fue exitoso.'
        }
        failure {
            echo 'El pipeline falló. Revisa los errores.'
        }
    }
}
