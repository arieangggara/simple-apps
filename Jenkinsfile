pipeline {
    agent { label 'dev-arie' }

    stages {
        stage('Pull SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/arieangggara/simple-apps.git'
            }
        }
        
        stage('Build') {
            steps {
                sh'''
                cd app
                npm install
                '''
            }
        }
        
        stage('Testing') {
            steps {
                sh'''
                cd app
                npm test
                npm run test:coverage
                '''
            }
        }
        
        stage('Code Review') {
            steps {
                sh'''
                cd app
               sonar-scanner \
  -Dsonar.projectKey=TESTSIMPLE \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://172.23.8.126:9000 \
  -Dsonar.login=sqp_19e3681eb347b16f0da6d010a8c1abcb83323de9
                '''
            }
        }
        
        stage('Deploy') {
            steps {
                sh'''
                docker compose up --build -d
                '''
            }
        }
        
        stage('Backup') {
            steps {
                 sh 'docker compose push' 
            }
        }
    }
}