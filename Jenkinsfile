pipeline {
    agent  any
    stages {
        stage('vcs') {
            steps {
                git branch: 'spc', url: 'https://github.com/all-projects-files/spring-petclinic.git'
            }

        }
        stage('build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('archive results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
    }

}