pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    echo "Current Branch Detected: ${env.BRANCH_NAME}"

                    if (env.BRANCH_NAME == 'nfs') {
                        echo "Running NFS Server Installation..."
                        sh "ansible-playbook -i nfs_hosts.in nfs.yml"
                    } 
                    else if (env.BRANCH_NAME == 'httpd' || env.BRANCH_NAME == 'main') {
                        echo "Running Apache Deployment..."
                        sh "ansible-playbook -i inventory.ini deploy-apache.yml --vault-password-file vault_pass.txt"
                    } 
                    else {
                        echo "No matching playbook found for branch ${env.BRANCH_NAME}."
                    }
                }
            }
        }
    }
}
