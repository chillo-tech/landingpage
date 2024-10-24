pipeline {
    agent any
    
    environment {
        fileName = 'file.txt'
        username = 'Achille'
        REPOSITORY = 'https://github.com/chillo-tech/landingpage.git'
        BRANCH = "main"
        EMAIL =  "achille.mbougueng@chillo.tech"
        USER_NAME = "chillo-tech"
        GIT_CREDENTIALS = credentials('github-chillotech-pat') 
    }

    parameters {
        string(name: "name", defaultValue: "user-card")
        text(name: "content")
        choice(name: "extension", choices: ['txt', 'docx'])
    }

    stages {
        stage ('Initialtisation') {
            steps {
                sh "printenv"
                git url: "${REPOSITORY}", branch: "${BRANCH}", credentialsId: 'github-chillotech-pat'
                sh "echo 'Content ${params.content}'"
            }
        }

        stage ('Create file') {
            steps {
               sh "echo ${params.content} > ${params.name}.${params.extension}"
            }
        }
        
        stage('Update commits') {
            steps {
                sh """
                    git config user.email ${env.EMAIL}
                    git config user.email ${env.EMAIL}
                    git config user.name ${env.USER_NAME}

                    git add .

                    git commit -am "Fichier ${params.name}.${params.extension}"
                """
            }
        }
        
        
        stage('check') {
            steps {
                sh 'ls -al'
            }
        }
    }
}
