pipeline {

    agent any

    tools {
        maven "Maven"
    }

    triggers {
        pollSCM "* * * * *"
    }

    parameters {
        booleanParam(name: "RELEASE",
                description: "Build a release from current commit.",
                defaultValue: false)
    }

    stages {

        stage("Build & Deploy SNAPSHOT") {
            steps {
                ansiColor("xterm") {
                    sh "mvn -B deploy"
                }
            }
        }

        stage("Release") {
            when {
                expression { params.RELEASE }
            }
            steps {
                ansiColor("xterm") {
                    sh "mvn -B release:prepare"
                    sh "mvn -B release:perform"
                }
            }
        }

    }

    post {
        always {
            deleteDir()
        }
    }
}