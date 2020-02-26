pipeline {
  agent { 
    kubernetes {
      label 'python-alpine-pod'
       yamlFile 'py-pod.yaml'
     }
  }  
  stages {
    stage ('Build') {
      steps {
        container ('python') {
          sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
      }
    }
  }
}
