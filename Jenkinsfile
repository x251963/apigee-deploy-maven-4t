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

                 stage("list") {
                         steps {
                             script {
                               sh "ls"
                               sh "rm -fr telus"
                               sh "whereis java"
                               sh "mvn --version"
                               sh "java -version"
                               sh "mkdir -p telus/archive/docs telus/archive/src telus/binaries  telus/build-artifacts telus/docs/customer telus/docs/reference telus/docs/solution telus/src telus/src telus/src telus/src/analytics telus/src/java telus/src/portal telus/src/gateway/parent-pom telus/src/gateway/test-app/apiproxy/proxies telus/src/gateway/test-app/apiproxy/resources/py telus/src/gateway/test-app/apiproxy/targets telus/src/gateway/test-app/apiproxy/policies telus/test"
                               sh "echo '============Directory===================='"
                             }
                         }

                 }
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
                        sh "mvn --version"
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
