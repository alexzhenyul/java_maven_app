#!/usr/bin/env groovy

def gv

pipeline {
    agent any
    tools {
        maven "maven-3.9"
    }
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages {
        stage("init") {
            steps {
                script {
                   gv = load "script.groovy"
                }
            }
        }
        stage("build") {
            steps {
                script {
                    echo "building the application"
                    gv.buildJar()
                }
            }
        }
        stage("build docker image") {
            steps {
                script {
                    echo "building docker images..."
                    gv.buildImage()
                }
            }
        }
        stage("deployApp") {
            steps {
                script {
                    env.ENV = input message: "Select the environment to deploy to", ok: "Done", parameters: [choice(name: 'ONE', choices: ['dev', 'staging', 'prod'], description: '')]

                    gv.deployApp()
                    echo "Deploying to ${ENV}"
                }
            }
        }
    }
}
