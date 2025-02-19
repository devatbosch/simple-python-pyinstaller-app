pipeline {
    agent any 
    stages {
        stage('Checkout') { 
            steps {
                echo 'Cloning repository...'
                git 'https://github.com/your-repo/sample-project.git'
            }
        }

        stage('Build') { 
            steps {
                echo 'Compiling Python source files...'
                sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'pytest tests/' 
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running static code analysis...'
                sh 'pylint sources/*.py'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating package...'
                sh 'tar -czf app.tar.gz sources/'
                stash(name: 'package', includes: 'app.tar.gz')
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'scp app.tar.gz user@server:/deploy/path/'
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Cleaning up workspace...'
                deleteDir()
            }
        }
    }
}
