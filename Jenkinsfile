pipeline{
  agent any
  tools{
    maven 'Maven3'
    jdk 'JDK17'
  }
  stages{
    stage('Checkout Code'){
      steps{
        git 'https://github.com/chandana-code-java/springboot-devops-demo.git'
      }
    }
    stage('Build'){
      steps{
        sh 'mvn clean package -DskipTests'
      }
    }
    stage('Build Docker Image'){
      steps{
        sh 'docker build -t springboot-devops-demo:latest .'
      }
    }
    stage('Run Docker Container'){
      steps{
        sh ''' 
          docker stop springboot-devops-demo || true
          docker rm springboot-devops-demo || true
          docker run -d -p 9090:8081 --name springboot-devops-demo springboot-devops-demo:latest
          '''
      }
    }
  }
  post{
    success{
      echo 'Application deployed successfully!'
    }
    failure{
      echo 'Build failed!'
    }
  }
}
