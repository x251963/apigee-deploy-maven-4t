pipeline {
        agent any
        tools {
                maven "Maven 3.8.4"
                jdk   "JAVA8"
        }
        environment {
            APIGEE_SA_CREDS = credentials("Jenkins_git_token4x251963")
            ORG = "apigee-deploy-maven"
            ENV = "eval"
        }
       stages {


                stage("initialize") {
                    steps {
                        withMaven(maven: "maven") {
                            sh "mvn --version"
                        }

                    }
                }
                stage ("Build") {
                      steps {
                        sh "mvn clean package"
                        sh "echo '============Build===================='"
                        sh "mvn --version"
                      }
                }

         stage("Deploy proxy bundle") {
                    steps {
                        withMaven(maven: "maven"){
			    sh "ls -la ./Mock-v1/"	
                            sh "echo '============COMP===================='"
                            sh "mvn install -Ptest -f ./Mock-v1/pom.xml -Dorg=${env.ORG} -Denv=${env.ENV}  -Dfile=${APIGEE_SA_CREDS}"
                        }
                    }
                }


        }
}
