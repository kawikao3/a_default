#!/usr/bin/env groovy

node() {
    stage('Download') {
        deleteDir()
        checkout scm
        git_commit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
    }

    stage('Dependencies') {
        env.GCE_CREDENTIALS="/var/lib/jenkins/.gcloud/credentials.json"
        env.GCE_PROJECT_ID="green-entity-167900"
        env.GCE_DEFAULT_ZONE="us-west1-a"
        env.GCE_SOURCE_IMAGE_FAMILY="ubuntu-1704"
        env.GCE_IMAGE_FAMILY="a-com-default"
        env.PACKER_LOG=0
    }

    stage('Unit Tests') {
    }

    stage('Build') {
        sh(returnStdout: true, script: 'packer build Packerfile.json')
    }
}
