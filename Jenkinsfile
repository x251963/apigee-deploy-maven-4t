pipeline {
        agent any
        environment {
            APIGEE_SA_CREDS = credentials("APIGEE_SA_CREDS")
            ORG = "cdo-ccai-apigee-np-7d4f08"
            ENV = "ccai-lab1"
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
                            sh "mvn install -Ptest -f ./Mock-v1/pom.xml -Dorg=${env.ORG} -Denv=${env.ENV}  -Dfile=\${APIGEE_SA_CREDS}"
                        }
                    }
                }

              
        }
}
