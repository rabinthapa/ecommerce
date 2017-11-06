pipeline {
    agent any

    tools {
        maven 'Maven 3.3.9'
        jdk 'jdk8'
    }
    stages {

        stage('Build') {
            steps {
                bat 'mvn clean install -DskipTests'
                stash 'working-copy'
            }
        }


        stage('Test') {
            steps {
                unstash 'working-copy'
                bat 'mvn test'
            }
        }


        stage('Code Quality') {
            steps {
                 unstash 'working-copy'
                 step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: '**/target/checkstyle-result.xml', unstableTotalAll:'0'])


            }
        }
    }
}