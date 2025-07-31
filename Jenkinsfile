pipeline {
    agent { label 'devops1-nama' }

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
                -Dsonar.projectKey=simple-arie1 \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://172.23.8.126:9000 \
                -Dsonar.login=sqp_fa3c341116c080b79559c9183982b9feeeeaee4dar.login=token-sonar
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