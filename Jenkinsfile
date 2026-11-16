pipeline {
    agent any
    stages {
        stage('Verify tag is on main') {
            when { expression { env.ref?.startsWith('refs/tags/') } }
            steps {
                sh '''
                    git fetch origin main --tags
                    TAG="${ref#refs/tags/}"
                    SHA=$(git rev-list -n 1 "$TAG")
                    git merge-base --is-ancestor "$SHA" origin/main
                '''
            }
        }
        stage('Prod Deploy') {
            steps {
                echo "Deploying release ${env.ref}"
            }
        }
    }
}
