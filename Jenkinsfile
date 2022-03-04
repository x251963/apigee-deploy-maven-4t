pipeline {
        agent any

        environment {
            APIGEE_SA_CREDS = credentials('Jenkins_git_token4x251963')
            ORG = 'apigee-deploy-maven'
            ENV = 'eval'
        }
       stages {
                stage('initialize') {
                    steps {
                        withMaven(maven: 'maven') {
                            sh "mvn --version"
                        }
                    }
                }
         stage('Deploy proxy bundle') {
                    steps {
                        withMaven(maven: 'maven'){
                            sh "mvn install -Ptest -f ./Mock-v1/pom.xml -Dorg=${env.ORG} -Denv=${env.ENV}  -Dfile=${APIGEE_SA_CREDS}"
                        }
                    }
                }

                stage('Deploy To Prod') {
                    input {
                        message "Do you want to proceed for production deployment?"
                    }
                    steps {
                        sh 'echo "Deploy into Prod"'
                    }
                }
        }
}