pipeline {
    agent any

    stages {
        stage('CHECKOUT') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/aafetorgbor/Python-app.git']]])
            }
        }

        stage('BUILD') {
            steps {
                echo "Building Image"
            }
        }

        stage('TEST') {
            steps {
                sh '''#!/bin/bash
                    echo "${WORKSPACE}"
                    echo $WORKSPACE
                    echo
                    pytest -v  --junitxml=result.xml

                  '''
            }

            post {
                always {
                     junit testResults: '*.xml', skipPublishingChecks: true
                }
            }

        }

        stage('DEPLOY') {
            steps {
                echo "Deploying"
            }
        }
    }
}


