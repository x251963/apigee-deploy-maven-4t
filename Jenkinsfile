pipeline {
        agent any
        environment {
            APIGEE_SA_CREDS = credentials("APIGEE_SA_CREDS")
            ORG = "48751253166@cloudbuild.gserviceaccount.com"
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

         stage("Deploy proxy bundle") {
                    steps {
                        withMaven(maven: "maven"){
                            sh "mvn install -Ptest -f ./Mock-v1/pom.xml -Dorg=${env.ORG} -Denv=${env.ENV}  -Dfile=${APIGEE_SA_CREDS}"
                        }
                    }
                }

              
        }
}
