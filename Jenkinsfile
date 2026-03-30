pipeline{
  agent any
  tools{
    java21 "java21"
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
