pipeline {
    agent any
    
    tools {nodejs "node11"}
    
    environment {
        CI = 'true'
    }
    stages {
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm run lint'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deliver') {
            steps {
				sh 'git add build && git commit -m "Initial build subtree commit"'
				sh 'git subtree push --prefix build origin gh-pages'
            }
        }
    }
}

