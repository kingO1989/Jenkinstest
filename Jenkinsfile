pipeline {
agent any

      environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }
    stages {
        stage('deploy') {
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

                           echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"

                       retry(3) {
                    bat './flakey-deploy.sh'
                       }

                timeout(time: 3, unit: 'MINUTES') {
                    bat './health-check.sh'
                         }
                   /* the Container gets removed */
                   bat "docker rm -f ${MY_CONTAINER}"

               
                        }
                    }
                }
            }
        }
