pipeline {

    agent any

    parameters {

        booleanParam(name: 'RUN_INTEGRATION_TESTS', defaultValue: true)

    }

    stages {

        stage('Tests') {

            parallel {

                stage('Unit tests') {

                    steps {

                        sh './mvnw test -D testGroups=unit'

                    }

                }

                stage('Integration tests') {

                    when {
                        
                        expression { return params.RUN_INTEGRATION_TESTS }

                    }

                    steps {

                        sh './mvnw test -D testGroups=integration'

                    }

                }

            }

        }

    }

    stage('Build') {

        steps {

            script {

                try {

                    sh './mvnw package -D skipTests'
                } catch (Exception ex) {

                    echo 'Error while generating JAR file'
                    throw exx
                }
            
            }

        }

    }

}