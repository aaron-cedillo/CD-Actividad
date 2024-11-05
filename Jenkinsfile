pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/aaron-cedillo/CD-Actividad.git'
    }

    stages {
        stage('Clonar Repositorio') {
            steps {
                // Clona el repositorio desde GitHub
                git REPO_URL
            }
        }

        stage('Verificar Archivos') {
            steps {
                script {
                    // Verifica que los archivos HTML y CSS existan en sus subdirectorios
                    if (!fileExists('HTML/index.html') || !fileExists('CSS/styles.css')) {
                        error "Archivos HTML o CSS no encontrados."
                    }
                }
            }
        }

        stage('Despliegue en Preproducción') {
            steps {
                // Simulación de despliegue en preproducción
                echo 'Desplegando en el entorno de Preproducción...'
            }
        }

        stage('Pruebas Automatizadas') {
            steps {
                // Ejecuta pruebas simples para validar que la página funciona
                script {
                    echo 'Ejecutando pruebas automatizadas...'
                    sh 'curl -I http://localhost:8080/HTML/index.html || exit 1'
                }
            }
        }

        stage('Despliegue en Producción') {
            steps {
                echo 'Desplegando en el entorno de Producción...'
                // Copia los archivos al directorio de producción
                sh 'rsync -avz HTML/index.html CSS/styles.css /var/www/html/'
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
