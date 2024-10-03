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
//                    passwd = "dhrcjs1871"
                    passwd = "dckr_pat_3lcy8ghqNEhsfSzQ0_9VYsBDwp0"
                }
                sh "echo $passwd | docker login -u $user --password-stdin $url"
                sh "docker push btjeon/calculator"
            }
        }
    }
}

