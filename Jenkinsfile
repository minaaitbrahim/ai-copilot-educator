pipeline {
    agent any
    
    environment {
      VENV_NAME = 'educopilot_venv'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MrMorad97/ai-copilot-educator.git'
                dir('Educopilot') {
                    sh 'cd Educopilot'
                }
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'pip3 install virtualenv'
                sh "python3 -m venv ${VENV_NAME}"
                sh "source ${VENV_NAME}/bin/activate"
                sh 'pip3 install langchain chromadb pypdf fastembed'
            }
        }
        
        stage('Launch Ollama Server') {
            steps {
                sh 'ollama --model mistral --serve' 
            }
        }
        
        stage('Run Streamlit Server') {
            steps {
                sh 'streamlit run server.py'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline succeeded! Servers are running.'
            // Optionally notify stakeholders or trigger further actions on success
        }
        failure {
            echo 'Pipeline failed! Check logs for details.'
            // Optionally notify stakeholders or handle failure gracefully
        }
    }
}
