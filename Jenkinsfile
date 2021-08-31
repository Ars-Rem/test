pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr:'3'))
        timeout(time: 30, unit: 'MINUTES')
//        ansiColor('gnome-terminal')
    }
    stages {
        stage ('Build') {
            when {
                expression {
                    return env.BRANCH_NAME != 'develop' && env.BRANCH_NAME != 'master' && env.BRANCH_NAME != 'stage';
                }
            }
            steps {
                sh 'npm i'
                sh 'npm run build'
             }
        }
         stage ('Build -  dev & deploy') {
            when {
                branch 'develop'
            }
             steps {
                 sh 'echo develop'
             }
         }   
         stage ('Build - stage') {
            when {
                branch 'stage'
            }
             steps {
                 sh 'echo ok'
             }
         }
         stage ('Build - prod') {
            when {
                branch 'master'
            }
             steps {
                 sh 'echo ok'
                 sh "npm install"
             }
         }
         stage ('Recycle') {
             steps {
                 sh 'rm -rf *'
            }
         }
    }
}
