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
                    // Verifica que los archivos HTML y CSS existan
                    if (!fileExists('index.html') || !fileExists('styles.css')) {
                        error "Archivos HTML o CSS no encontrados."
                    }
                }
            }
        }

        stage('Despliegue en Preproducción') {
            steps {
                // Simulación de despliegue en preproducción
                echo 'Desplegando en el entorno de Preproducción...'
                // Aquí podrías agregar comandos de despliegue específicos de tu entorno preproducción
            }
        }

        stage('Pruebas Automatizadas') {
            steps {
                // Ejecuta pruebas simples para validar que la página funciona
                script {
                    echo 'Ejecutando pruebas automatizadas...'
                    sh 'curl -I http://localhost:8080/index.html || exit 1'
                }
            }
        }

        stage('Despliegue en Producción') {
            steps {
                echo 'Desplegando en el entorno de Producción...'
                sh 'rsync -avz index.html styles.css /var/www/html/'
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
