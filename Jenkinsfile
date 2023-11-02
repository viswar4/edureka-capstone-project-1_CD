pipeline{
    agent any
    environment{
        DOCKER_HUB_CREDENTIALS = 'dockerhub'
        DOCKER_IMAGE_NAME = 'viswar4/edureka-project1'
        DOCKER_IMAGE_TAG = "${env.BUILD_ID}"
        DOCKER_IMAGE = "${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
        WORKSPACE="${env.WORKSPACE}"
        VAULT_PASSWORD = credentials('ansiblevault')
           }

    stages{
        stage('Run Ansible playbook to create deploy, service and deploy to Kubernetes Cluster'){
        steps{
                ansiblePlaybook extras: '-e DOCKER_IMAGE_TAG=${DOCKER_IMAGE_TAG} -e WORKSPACE=${WORKSPACE}', 
                installation: 'ansible', 
                playbook: 'deploytokubernetes.yaml',
                vaultCredentialsId: 'ansiblevault'
            }
    }
    }
}