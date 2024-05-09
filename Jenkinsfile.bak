pipeline {
    agent any

    environment {
        // Define the default Python interpreter
        PYTHON = "py"
    }

    stages {
        stage('Check Python') {
            steps {
                echo 'Checking Python installation...'
                script {
                    // Check Python version
                    if (isUnix()) {
                        sh "${env.PYTHON} --version"
                    } else {
                        bat "${env.PYTHON} --version"
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing required Python packages...'
                script {
                    // Install Python dependencies
                    if (isUnix()) {
                        sh "${env.PYTHON} -m pip install -r requirements.txt"
                    } else {
                        bat "${env.PYTHON} -m pip install -r requirements.txt"
                    }
                }
            }
        }

        stage('Run Python Scripts') {
            steps {
                echo 'Running Python scripts...'
                script {
                    // Execute Python scripts
                    dir('conf') { // Change to the directory where the scripts are located
                        if (isUnix()) {
                            sh "${env.PYTHON} hello.py"
                            sh "${env.PYTHON} sum.py"
                        } else {
                            bat "${env.PYTHON} hello.py"
                            bat "${env.PYTHON} sum.py"
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
        always {
            echo 'Pipeline is complete.'
        }
    }
}
