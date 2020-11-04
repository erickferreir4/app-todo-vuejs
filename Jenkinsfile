pipeline {
  agent any
    
  tools {nodejs "node11"}
    
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
            sh 'rm -rf .git'
			dir('./build') {
            	sh 'git init'
            	sh 'git add .'
            	sh 'git commit -m "Deploy from Jenkins"'
            	sh 'git push --force --quiet "https://${GH_TOKEN}@github.com/erikferreir4/app-todo-vuejs.git" master:gh-pages '
			}
        }
    }
    
    
  }
}
