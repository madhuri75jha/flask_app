pipeline {
  agent { label 'linux-agent-new' }
  environment {
    VENV = 'venv'
  }
  stages {
    stage('Checkout Code') {
      steps {
        git branch: 'main', url: 'https://github.com/madhuri75jha/flask_app.git'
      }
    }
    stage('Setup Python Environment') {
      steps {
        sh '''
        python3 -m venv $VENV
        .$VENV/bin/activate
        pip install --upgrade pip
        '''
      }
    }
    stage('Install Dependencies') {
      steps {
        sh '''
        .$VENV/bin/activate
        pip install -r requirements.txt
        '''
     }
    }
    stage('Run Tests') {
      steps {
        sh '''
        .$VENV/bin/activate
        echo "NO TESTS defined yet - SKIPPING"
        '''
      }
    }
    stage('Run Flask Application') {
      steps {
        sh '''
        .$VENV/bin/activate
        echo "Starting FLASK APP..."
        python app.py &
        '''
      }
    }
  }
post {
  success {
    echo 'Flask CI/CD pipeline executed successfully'
      }
  failure {
    echo 'PIPELINE FAILED!!! Check LOGS'
  }
}
}
