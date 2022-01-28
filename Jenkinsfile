// los comentarios se ponen con //
    
pipeline {
    
    agent any // para que se pueda ejecutar en cualquer sitio
    
    stages {
        stage("Etapa 1") {
        
            steps { // hacemos las llamadas a los plugins
                sh "echo Soy la etapa 1"
            }
            post {
                always { // post tareas que siempre tienen que ejecutarse
                    sh "echo Acabó la etapa 1"    
                }
                succes { // post tareas que se ejecutan solo si los pasos han acabo bien
                    sh "echo Y acabo bien"
                }
                failure { // post tareas que se ejecutan solo si los pasos han acabao con error
                    sh "echo Pero acabó mal"
                }
            }
        }
        
        stage("Etapa 2") {
            steps {
                 sh """
                    echo Soy la etapa 2 
                    echo trabajando en etapa 2
                 """    
            }
            post {
                always { // post tareas que siempre tienen que ejecutarse
                    sh "echo Acabó la etapa 2"    
                }
            }
        }    
    }
}