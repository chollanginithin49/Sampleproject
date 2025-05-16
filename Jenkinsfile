pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/chollanginithin49/Sampleproject.git'
        BRANCH = 'bugfix'
        BUILD_DIR = 'target'
        RELEASE_DIR = 'release-artifacts'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Release') {
            steps {
                echo 'Releasing the build artifact...'
                sh '''
                    mkdir -p ${RELEASE_DIR}
                    cp ${BUILD_DIR}/*.jar ${RELEASE_DIR}/
                    echo "Artifacts copied to ${RELEASE_DIR}"
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and release completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
