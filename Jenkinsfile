pipeline{
    agent{
        kubernetes{
            cloud 'kubernetes'
            yamlFile 'pod.yaml'
            label 'react-agent'
            defaultContainer 'react'
            podRetention never()
        }
    }
    options{
        skipDefaultCheckout()
    }
    stages{
        stage('checkout'){
            steps{
                git branch:'main',url:'https://github.com/VinYuvian/fiberReact_front.git'
            }
        }

        stage('build'){
            steps{
                sh 'npm install'
                sh 'npm run build'
            }
        }
    }
}