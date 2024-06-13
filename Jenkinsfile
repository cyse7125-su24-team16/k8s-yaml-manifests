pipeline {
    agent any
 
     environment {
        GITHUB_CREDENTIALS_ID = 'github_token'
        DOCKER_CREDENTIALS_ID = 'docker_credentials'
        JENKINS_ADMIN_CREDENTIALS_ID = 'jenkins_credentials'
    }
 
    stages {
        stage('Checkout PR Branch') {
            steps {
                script {
                    // Fetch the latest changes from the origin using credentials
                    withCredentials([usernamePassword(credentialsId: GITHUB_CREDENTIALS_ID, usernameVariable: 'GITHUB_USER', passwordVariable: 'GITHUB_TOKEN')]) {
                        sh 'git config --global credential.helper store'
                        sh 'echo "https://${GITHUB_USER}:${GITHUB_TOKEN}@github.com" > ~/.git-credentials'
                        // Fetch all branches including PR branches
                        sh 'git fetch origin +refs/pull/*/head:refs/remotes/origin/pr/*'
                        // Dynamically fetch the current PR branch name using environment variables
                        def prBranch = env.CHANGE_BRANCH
                        echo "PR Branch: ${prBranch}"
                        // Checkout the PR branch
                        sh "git checkout -B ${prBranch} origin/pr/${env.CHANGE_ID}"
                    }
                }
            }
        }
 
        stage('Check Commit Messages') {
            steps {
                script {
                    // Fetch the latest commit message in the PR branch
                    def latestCommitMessage = sh(script: "git log -1 --pretty=format:%s", returnStdout: true).trim()
                    echo "Latest commit message: ${latestCommitMessage}"
 
                    // Regex for Conventional Commits
                    def pattern = ~/^\s*(feat|fix|docs|style|refactor|perf|test|chore)(\(.+\))?: .+\s*$/
 
                    // Check the latest commit message
                    if (!pattern.matcher(latestCommitMessage).matches()) {
                        error "Commit message does not follow Conventional Commits: ${latestCommitMessage}"
                    }
                }
            }
        }
 
        stage('Compare Changes') {
            steps {
                script {
                    // Compare the PR branch with the main branch
                    def diff = sh(script: 'git diff origin/main...HEAD', returnStdout: true).trim()
                    echo "Git Diff: ${diff}"
                    if (diff == "") {
                        echo "No differences found."
                    } else {
                        echo "Differences found:\n${diff}"
                    }
                }
            }
        }
   
       stage('YAML Lint') {
            steps {
                script {
                    // Lint the YAML files and capture output
                    def result = sh(script: 'yamllint k8s-manifests/ > yamllint_output.log 2>&1', returnStatus: true)
                    echo "yamllint exit code: ${result}"
                    sh 'cat yamllint_output.log'
                   
                    // Check if yamllint failed
                    if (result != 0) {
                        error 'YAML linting failed'
                    }
                }
            }
        }
    }
 
    }
   
    post {
        always {
            // Clean up workspace
            cleanWs()
        }
        failure {
            // Notify of failure
            echo 'YAML linting failed. Please check the linting errors and fix them.'
        }
    }
}
 