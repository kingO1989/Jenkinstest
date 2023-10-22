pipeline {
agent any
    stages {
        stage('build') {
            steps {
                script {
                   /* the return value gets caught and saved into the variable MY_CONTAINER */
                   MY_CONTAINER = bat(script: '@docker run -d -i node:18.18.2-alpine3.18', returnStdout: true).trim()
                   echo "mycontainer_id is ${MY_CONTAINER}"
                                 
                   bat "node --version"
                    bat '''
                    echo "Multiline shell steps works too"
                    dir
                '''
                   /* the Container gets removed */
                   bat "docker rm -f ${MY_CONTAINER}"
                        }
                    }
                }
            }
        }
