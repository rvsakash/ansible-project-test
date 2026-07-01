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
                    
                    if (env.BRANCH_NAME == 'nfs' || env.BRANCH_NAME == 'nfs-new') {
                        echo "Running NFS Server Installation with Vault..."
                        // Yahan humne vault password file ko jod diya hai
                        sh "ansible-playbook -i nfs_hosts.in nfs.yml --vault-password-file vault_pass.txt"
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
