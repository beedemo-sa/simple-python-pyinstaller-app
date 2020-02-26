pipeline {
  agent { 
    kubernetes {
      label 'python-alpine-pod'
       yamlFile 'py-pod.yaml'
     }
  }
  options {
    skipStagesAfterUnstable()
  }
  stages {
    stage ('Build') {
      steps {
        container ('python') {
          sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
      }
    }
    stage ('Test') {
      steps {
        container ('pytest') {
          sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        }
      }
      post {
        always {
          junit 'test-reports/results.xml'
        }
      }
    }
    stage ('Deliver') {
      steps {
        container ('pyinstaller') {
          echo 'pyinstaller --onefile sources/add2vals.py'
        }
      }
      post {
        success {
          echo 'archiveArtifacts dist/add2vals'
        }
      }
    }
  }
}
