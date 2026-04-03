pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/2025sl93028/labsheet1-2025sl93028.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo Build Stage'
                sh 'python3 --version'
            }
        }

        stage('Test') {
            steps {
                sh '''
                python3 -c "
import calculator

print('Testing add...')
assert calculator.add(2, 4) == 6

print('Testing multiply...')
assert calculator.multiply(2, 3) == 6

print('Testing divide...')
assert calculator.divide(6, 3) == 2

print('Testing subtract...')
assert calculator.subtract(5, 3) == 2

print('All tests passed successfully')
"
                '''
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                    scp -o StrictHostKeyChecking=no calculator.py ec2-user@16.170.229.151:/home/ec2-user/
                    ssh -o StrictHostKeyChecking=no ec2-user@16.170.229.151 "python3 calculator.py"
                    '''
                }
            }
        }
    }
}
