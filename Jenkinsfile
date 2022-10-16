pipeline {
    agent { label 'jdk11' }
     triggers { cron('30 5 * * *') }
    stages {
        stage('vcs') {
            steps {
                git branch: 'relese', url:'https://github.com/srvarri/shopizer.git'
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