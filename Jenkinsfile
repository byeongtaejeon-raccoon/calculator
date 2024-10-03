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
                def registry_url = "registry.hub.docker.com/"
                sh "docker login ${registry_url}"
                sh "docker push btjeon/calculator"
            }
        }
    }
}

