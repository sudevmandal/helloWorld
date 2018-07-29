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
                    zip -r HelloWorldJSP.1.0.0.zip HelloWorldJSP.war
                '''
                
            }
        }

        stage ('Deploy to Octopus') {
            steps {
                withCredentials([string(credentialsId: 'OctopusAPIKey', variable: 'APIKey')]) {
                    sh """
                    cd HelloWorldJSP
                    ls
                        ${tool('Octo CLI')}/Octo push --package HelloWorldJSP/HelloWorldJSP.1.0.0.zip --replace-existing --server http://ec2-54-146-131-176.compute-1.amazonaws.com --apiKey ${APIKey}                        
                    """
                }
            }
        }
    }
}
