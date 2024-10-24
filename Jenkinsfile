pipeline {
    agent {
        docker {
            image 'node:20-alpine'
        }
    }
    
    environment {
        fileName = 'file.txt'
        username = 'Achille'
        GIT_CREDENTIALS = credentials('github')
    }

    parameters {
        string(name: "file", defaultValue: "user-card")
        text(name: "content")
        choice(name: "extension", choices: ['txt', 'docx'])
    }

    stages {
        stage ('Initialtisation') {
            steps {
                 git url: 'https://github.com/chillo-tech/landingpage.git',
                    credentialsId: 'github-pat', 
                    branch: 'main'
                
                sh "echo 'File ${params.name}'"
                sh "echo 'Extension ${params.extension}'"
                sh "echo 'Content ${params.content}'"
                sh "printenv"
            }
        }

        stage('build') {
            when {
                environment name: "file", value : "index"
            }
            steps {
                sh "echo 'Hello ${env.username}' > ${params.file}.${params.extension}"
            }
        }
        
        stage('test') {
            steps {
                sh 'ls -al'
                sh '''
                    npm --version
                '''
            }
        }
        
        
        stage('check') {
            steps {
                sh 'ls -al'
            }
        }
    }
}
