pipeline {
    agent linux_node

    environment {
        PY_ENV_PATH = 'python_environment'  // Folder for the virtual environment
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Cloning repo...'
                git branch: 'master', url: 'https://github.com/rahulreghunathOrg/Jenkins-Python-Pipeline-demo.git'
            }
        }

        stage('Set Up Python Environment') {
            steps {
                echo "Creating virtual environment at ${PY_ENV_PATH}..."
                sh '''
                    python3 -m venv ${PY_ENV_PATH}
                    . ${PY_ENV_PATH}/bin/activate
                    pip install --upgrade pip
                '''
            }
        }

        stage('Run Hello Test') {
            steps {
                echo "Running a basic Python test..."
                sh '''
                    . ${PY_ENV_PATH}/bin/activate
                    echo "print('Hello from Jenkins Pipeline!')" > hello.py
                    python hello.py
                '''
            }
        }
    }

    post {
        always {
            echo '🧹 Cleaning up...'
            sh 'rm -rf ${PY_ENV_PATH} hello.py'
        }
        success {
            echo '🎉 Build and test ran successfully!'
        }
        failure {
            echo '❌ Build failed — check the logs above.'
        }
    }
}
