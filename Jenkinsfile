pipeline {
    agent any
    stages {
        stage("Compile") {
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage("Unit test") {
            steps {
                sh "./gradlew test"
            }
        }
        stage("Package") {
            steps {
                sh "./gradlew build"
            }
        }
        stage("Docker build") {
            steps {
                sh "docker build -t btjeon/calculator ."
            }
        }
        stage("Docker push") {
            steps {
                script {
                    url = "registry.hub.docker.com/"
                    user = "btjeon"
                    passwd = "dckr_pat_3lcy8ghqNEhsfSzQ0_9VYsBDwp0"
                }
                sh "echo $passwd | docker login -u $user --password-stdin $url"
//                sh "docker push btjeon/calculator"
            }
        }
        stage("Deploy to staging") { 
            steps { 
                sh "docker run -d --rm -p 8765:8080 --name calculator btjeon/calculator" 
            } 
        }
        stage("Acceptance test") { 
            steps { 
                sleep 60 
//                sh "chmod +x acceptance_test.sh && ./acceptance_test.sh"
                sh "./gradlew acceptanceTest -Dcalculator.url=http://localhost:8765"
            } 
       }
    }
    post { 
        always { 
            sh "docker stop calculator"
//             sh "echo 'end'"
        } 
    }
}

