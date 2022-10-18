pipeline {
    agent { label 'jdk11' }
     triggers { cron('0 5 * * *') }
    stages {
        stage('vcs') {
            steps {
                git branch: 'relese', url:'git@github.com:srvarri/shopizer.git'
            }

        }
       stage('MERGE') {
            steps {
                sh 'git checkout relese'
                sh 'git merge develop --no-ff'
                sh 'git push -u origin relese'
            }
        }
        stage('build') {
            steps {
                sh '/usr/share/maven/bin/mvn package'
            }
        }

        stage('archive results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
		stage ( 'artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar'
            }
		}
    }    
}    
