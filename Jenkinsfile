// los comentarios se ponen con //
    
pipeline {
    
    agent any // para que se pueda ejecutar en cualquer sitio
    
    stage("Etapa 1") {
        steps { // hacemos las llamadas a los plugins
            sh "echo Soy la etapa 1"
        }
    }
    
    stage("Etapa 2") {
        steps {
             sh """
             echo Soy la etapa 2
             echo Acabo la etapa 2
             """    
        }
    }
}