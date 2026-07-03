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
                    echo "Running NFS Server Installation with Vault..."
                    
                    // Main aur nfs-new dono par ab NFS setup hi chalega
                    sh 'ansible-playbook -i nfs_hosts.in nfs.yml --vault-password-file /opt/ansible-project-test/vault_pass.txt'
                }
            }
        }
    }
}
