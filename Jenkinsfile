pipeline{
  agent any
  tools{
    jdk "java21"
    nodejs "nodejs"
  }
  stages{
    stage("cleaning workspace"){
      steps{
        cleanWs()
      }
    }
  }
}
