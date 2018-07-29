pipeline {
    agent any
    
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "ANT_HOME = ${ANT_HOME}"
                '''
            }
        }

        stage ('Build') {
            steps {
                sh '''
                    cd HelloWorldJSP
                    ant -v
                '''
                
            }
        }

        stage ('Deploy to Octopus') {
            steps {
                withCredentials([string(credentialsId: 'OctopusAPIKey', variable: 'APIKey')]) {
                    sh """
                        ${tool('Octo CLI')}/Octo push --package helloWorld.war --replace-existing --server http://ec2-54-146-131-176.compute-1.amazonaws.com --apiKey ${APIKey}                        
                    """
                }
            }
        }
    }
}
