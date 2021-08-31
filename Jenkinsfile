pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr:'3'))
        timeout(time: 30, unit: 'MINUTES')
        ansiColor('gnome-terminal')
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
                 sh "npm install"
                 sh "npm run build"
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
         stage ('Build - prod && deploy') {
            when {
                branch 'master'
            }
             steps {
                 sh "npm install"
                 sh "npm run build"
                 sh "rsync --archive /var/lib/jenkins/workspace/test/build/* test2@192.168.3.233:/var/www/html/"  
             }
         }
         stage ('Recycle') {
             steps {
                 sh 'rm -rf *'
            }
         }
    }
}
