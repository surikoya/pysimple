pipeline {
    /* insert Declarative Pipeline here */
    agent {
      label 'python3'
    }
    stages {
      stage('Build') {
        steps {
          sh 'python -m py_compile src/*.py'
        }
      }

      stage('Test') {
        steps {
	  sh 'py.test --verbose --junit-xml test-reports/results.xml src/test.py'   
	}
	post {
	  always {
	    junit 'test-reports/results.xml'
	  }
	}
      }

      stage('Deliver') {
        steps {
	  sh 'pyinstaller --onefile src/*.py'
	}
	post {
	  success {
	    archiveArtifacts 'dist/final-artifact'
	  } 
	}
      }

    }
}
