pipeline {
    agent  any //{ label 'OPENJDK-11-MAVEN' }
    parameters {
        choice(name: 'BRANCH_TO_BUILD', choices: ['spc', 'main'], description: 'Branch to build')
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')

    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/all-projects-files/spring-petclinic.git'
            }
            
        }
        stage('build') {
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('archive results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
        stage('reports') {
            steps {
                jacoco()
            }
        }
    }
}