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
    stage("git checkout"){
      steps{
        git branch: "main", url: "https://github.com/Rutvikgalale/swiggy-app.git"
      }
    }
  }
}
