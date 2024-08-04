pipeline {
    agent any

    tools {
        // Install the Maven version configured as "maven-398" and add it to the path.
        maven "maven-398"
    }

    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'http://localhost:3000/dasher-org/jenkins-hello-world.git'
                sh "mvn clean package -DskipTests=true"
            }
        }

        stage('Unit Test') {
            steps {
                sh "mvn test"
                junit testResults: 'target/surefire-reports/TEST-*.xml'
            }
        }

        stage('Local Deployment') {
        steps {
            sh """ java -jar target/hello-demo-*.jar > /dev/null & """
            }
        }
    
        stage('Integration Testing') {
        steps {
            sh "sleep ${params.SLEEP_TIMER}"
            sh """ curl -s http://localhost:${params.APPLICATION_PORT}/hello | grep -i "Hello, KodeKloud community!" """
            }
        }

    }
}
