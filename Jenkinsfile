pipeline {
    agent any

    triggers {
        cron('H/10 * * * 4')
    }

    stages {
        stage('Cloning git') {
            steps {
                 git branch: 'main', url: 'https://github.com/jmarmol1/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    sh './mvnw clean package'
                }
            }
        }

        stage('Code Coverage (JaCoCo)') {
            steps {
                jacoco(
                      execPattern: 'target/*.exec',
                      classPattern: 'target/classes',
                      sourcePattern: 'src/main/java',
                      exclusionPattern: 'src/test*'
                )
            }
        }

    }
}