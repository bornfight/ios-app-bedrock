pipeline {
    agent {
        label "osx"
    }
    environment {
        LANG = 'en_US.UTF-8'
        LANGUAGE = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }
    stages {
        stage("Bitbucket checkout") {
            steps {
                msg =  "Started building ${env.APP_IDENTIFIER}. <${env.BUILD_URL}/console|View console>"
                slackSend channel: '#ios-dev', color: '#42dd45', message: msg, tokenCredentialId: 'moj-mali-ios-slack-notifier'

                checkout([$class: 'GitSCM', branches: [[name: "*/${env.APP_GIT_BRANCH}"]], doGenerateSubmoduleConfigurations: false, extensions: [[$class: "CleanBeforeCheckout"]], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'bitbucket-pvt', url: "${env.APP_GIT_URL}"]]])
            }
        }

        stage("Lint") {
            steps {
                sh "fastlane lint"
            }
        }      

        stage("Test") {
            steps {
                sh "fastlane test"
            }
        }      

        stage("Build") {
            steps {
                sh "fastlane build ci:true"
            }
        }      

        stage("Distribute") {
            steps {
                sh "fastlane distribute method:${env.APP_DISTRIBUTION_METHOD}"
            }
        }      

        post {
            success {
                msg = "Successfuly built ${env.APP_IDENTIFIER}. <${env.BUILD_URL}|Link to build>"
                slackSend channel: '#ios-dev', color: 'good', message: msg, tokenCredentialId: 'moj-mali-ios-slack-notifier'
            }

            failure {
                msg = "Failed to build ${env.APP_IDENTIFIER}. <${env.BUILD_URL}|Link to build>"
                slackSend channel: '#ios-dev', color: 'bad', message: msg, tokenCredentialId: 'moj-mali-ios-slack-notifier'
            }
        }
    }
    options {
        ansiColor("xterm")
        timestamps()
    }
}
