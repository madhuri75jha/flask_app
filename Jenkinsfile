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
        sudo apt update
        sudo apt install -y python3-venv

        python3 -m venv $VENV
        . $VENV/bin/activate
        pip install --upgrade pip
        '''
      }
    }

    stage('Install Dependencies') {
      steps {
        sh '''
        . $VENV/bin/activate
        pip install -r requirements.txt
        '''
      }
    }

    stage('Run Tests') {
      steps {
        sh '''
        . $VENV/bin/activate
        echo "NO TESTS defined yet - SKIPPING"
        '''
      }
    }

    stage('Run Flask Application') {
      steps {
        sh '''
        . $VENV/bin/activate
        echo "Starting FLASK APP..."
        nohup python app.py > app.log 2>&1 &
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
