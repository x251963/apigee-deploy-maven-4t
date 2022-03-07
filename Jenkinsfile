pipeline {
        agent any
        environment {
            APIGEE_SA_CREDS = credentials("APIGEE_SA_CREDS  ")
            ORG = "apigee-deploy-maven"
            ENV = "eval"
        }
       stages {

                stage("initialize") {
                    steps {
                        withMaven(maven: "MAVEN") {
                            sh "mvn --version"
                        }

                    }
                }

         stage("Deploy proxy bundle") {
                    steps {
                        withMaven(maven: "MAVEN"){
                            sh "mvn install -Ptest -f ./Mock-v1/pom.xml -Dorg=${env.ORG} -Denv=${env.ENV}  -Dfile=${APIGEE_SA_CREDS}"
                        }
                    }
                }

              
        }
}
