pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'python3 -m py_compile sources/add2vals.py sources/calc.py'
		stash(name: 'compile-results', includes: 'sources/*.py*')
            }
        }

	stage('Test') {
             steps {
                sh 'py.test --junit-xml test-reports/result.xml sources/test_calc.py'
            }
	     post {
		always {
		    junit 'test-reports/result.xml'
			} 
		}
        }

	stage('Deliver') {
             steps {
                sh 'pyinstaller --onefile sources/add2vals.py'
                    }
		post {
                	success { archiveArtifacts 'dist/add2vals'
  		      }

}}

    }
}
