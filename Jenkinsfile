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
    environment{
        image_name = 'vin1711/fiber_react_frontend'
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
        
        stage('Create docker Image'){
            steps{
                container('docker'){
                    sh "docker build -t ${image_name}:${BUILD_ID} -t ${image_name}"
                    withCredentials([usernamePassword(credentialsId:'dockerCred',usernameVariable:'user',passwordVariable:'passwd')]){
                        sh "docker login -u $user -p $passwd"
                        sh "docker push ${image_name}:${BUILD_ID}"
                        sh "docker push ${image_name}"
                    }
                }
            }
        }
    }
}
