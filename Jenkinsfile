pipeline {
    
    agent any
    
    stages {
        stage("Compilación") {
            steps {
                sh "mvn compile"
            }
            
        }
        stage("Pruebas") {
            stages {
                stage("Pruebas Dinámicas") {
                    /* Solucion con MAGIA... evitar                    
                    steps {
                        // Compilar pruebas -> Las pruebas no pueden ejecutarse
                        // Ejecutar pruebas -> Genera informe... tanto si se ejecutan bien como si se ejecutan mal
                    }
                    post {
                        always {
                            junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml' 
                        }    
                    }
                    */       
                    stages {
                        stage("Compilación pruebas") {
                            steps {
                                // Compilar pruebas -> Las pruebas no pueden ejecutarse
                                sh "mvn test-compile"
                            }
                        }
                        stage("Ejecución pruebas") {
                            steps {
                                // Ejecutar pruebas -> Genera informe... tanto si se ejecutan bien como si se ejecutan mal
                                sh "mvn test"
                            }
                            post{
                                always {
                                    // Guardar el informe de pruebas <- 
                                    junit testResults: "target/surefire-reports/*.xml"
                                }    
                            }
                        }
                    }
                }
                stage("SonarQube") {
                    // Sonarqube
                    steps {
                        withSonarQubeEnv('sonarqube'){ 
                            sh """
                            mvn sonar:sonar \
                                -Dsonar.projectKey=proyectoMaven \
                                -Dsonar.host.url=http://172.31.11.22:8081 \
                                -Dsonar.login=e0d05b1445cc1113e967f7da44a7c3861d0cd60e
                            """
                        }
                        timeout(time: 10, unit: "MINUTES"){
                            waitForQualityGate abortPipeline: true    
                        }
                    }
                    
                }
            }
        }
        stage("Empaquetado") {
            steps {
                // Empaquetar
                sh "mvn package -Dmaven.test.skip=true"
            }
            post{
                success {
                    // Guardar el artefacto (resultante del empaquetado)
                    archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
                    
                    
                }
            }
        }
    }
    post {
        always {
            // Borrar el espacio de trabajo
            cleanWs deleteDirs: true, patterns: [[pattern: 'target', type: 'INCLUDE']]
        }
    }
}