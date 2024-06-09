pipeline {
    agent any

    stages {
        stage('Clonar el Repositorio'){
            steps {
                git branch: 'main', url: 'https://github.com/MagdaDuqueIUD/proyectojenkins.git'
            }
        }
        stage('Construir imagen de Docker'){
            steps {
                script {
                    {
                        docker.build('proyectojenkins:v1', '--build-arg MONGODB_URI=${MONGODB_URI} .')
                    }
                }
            }
        }
        stage('Desplegar contenedores Docker'){
            steps {
                script {
                    {
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Status del build: ${currentBuild.currentResult}",
                body: "Se ha completado el build. Puede detallar en: ${env.BUILD_URL}",
                to: "maria.duquemr@est.iudigital.edu.co",
                from: "jenkins@iudigital.edu.co"
            )
        }
    }
} 