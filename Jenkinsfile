pipeline{
  agent any
  tools{
    maven 'Maven3'
    jdk 'JDK17'
  }
  stages{
    stage('Checkout Code') {
  steps {
    git branch: 'feature_springboot_demo', url: 'https://github.com/chandana-code-java/springboot-devops-demo.git'
  }
}
    stage('Build'){
      steps{
        bat 'mvn clean package -DskipTests'
      }
    }
    stage('Build Docker Image'){
      steps{
        bat 'docker build -t springboot-devops-demo:latest .'
      }
    }
    stage('Run Docker Container'){
      steps{
        bat ''' 
          docker stop springboot-devops-demo || exit 0
          docker rm springboot-devops-demo || exit 0
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
