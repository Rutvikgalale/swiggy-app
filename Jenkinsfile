pipeline{
  agent any
  tools{
    jdk "java21"
    nodejs "nodejs"
  }
  environment{
    SCANNER_HOME=tool("sonar-scanner")
  }
  stages{
    stage("cleaning workspace"){
      steps{
        cleanWs()
      }
    }
    stage("git checkout"){
      steps{
        git branch: "main", url: "https://github.com/Rutvikgalale/swiggy-app.git"
      }
    }
    stage("sonarqube analysis"){
      steps{
        withSonarQubeEnv("sonar-server"){
          sh """
            $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=swiggy-app -Dsonar.projectKey=swiggy-app \
            -Dsonar.sources=src 
          """
        }
      }
    }
    stage("Quality Gate"){
      steps{
        script{
          waitForQualityGate abortPipeline: false, credentialsId: "sonar-token"
        }
      }
    }
    stage("installation of dependencies"){
      steps{
        sh "npm install"
      }
    }
    stage("TRIVY FS SCAN"){
      steps{
        sh "trivy fs . > trivyfs.txt"
      }
    }
    stage("docker build & push"){
      steps{
        script{
          withDockerRegistry(credentialsId: "docker", toolName: "docker"){
            sh """
            docker build -t swiggy-app .
            docker tag swiggy-app:latest rutvikg/swiggy-app:latest
            docker push rutvikg/swiggy-app:latest
            """
          }
        }
      }
    }
  }
}
