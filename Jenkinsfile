pipeline {
        agent any
        tools {
                 jdk   "JAVA8"
                 maven "Maven 3.8.4"    
        }
        environment {
            APIGEE_SA_CREDS = credentials('APIGEE_SA_CREDS')
            ORG = "apigee-deploy-maven"
            ENV = "eval"
        }
       stages {


                stage('initialize') {
                    steps {
                        withMaven(maven: 'maven') {
                            sh "mvn --version"
                        }

                    }
                }
                stage ("Build") {
                      steps {
                        sh "mvn clean package"
                        sh "mvn --version"
                      }
                }

         stage("Deploy proxy bundle") {
                    steps {
                        withMaven(maven: 'maven'){                 
                            sh "mvn install -Ptest -f ./Mock-v1/pom.xml -Dorg=${env.ORG} -Denv=${env.ENV}  -Dfile=\${APIGEE_SA_CREDS}"
                        }
                    }
                }

                stage("Deploy To Prod") {
                    input {
                        message "Do you want to proceed for production deployment?"
                    }
                    steps {
                        sh "echo \"Deploy into Prod\""
                    }
                }
        }
}
