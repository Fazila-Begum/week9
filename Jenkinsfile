pipeline{
    agent any
    stages{
      stage('Build Docker Inage'){
        steps{
          echo "Build Docker Image"
          bat "docker build -t kubdemo:v1 ."
        }
      }
      stage('Dokcer Login'){
        steps{
            bat "docker login -u fazilabegum -p admin@123"
        }
      }
      stage('push Docker Image to Docker Hub'){
        steps{
            echo "push Docker Image to Docker Hub"
            bat "docker tag kubdemo:v1 fazilabegum/sample:kubeimage1"
            bat "docker push fazilabegum/sample:kubeimage1"
        }
      }
      stage('Deploy to kubernetes'){
        steps{
            bat "kubectl apply -f deployment.yaml --validate=false"
            bat "kubectl apply -f service.yaml"
        }
      }
    }
    post{
        success{
            echo 'Pipeline completed successfully!'
        }
        failure{
            echo 'Pipeline failed. Please check the logs.'
        }
    }

}

