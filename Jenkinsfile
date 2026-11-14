
pipeline {
    agent any

    stages {
        stage('Build Information') {
            steps {
                echo "Job Name: ${env.JOB_NAME}"
                echo "Build Number: ${env.BUILD_NUMBER}"
            }
        }

        stage('Disk Monitoring') {
            steps {
                sh '''
                    echo "Checking disk usage..."

                    df -h /

                    DISK_USAGE=$(df -P / | awk 'NR==2 {gsub("%","",$5); print $5}')

                    echo "Disk Usage: ${DISK_USAGE}%"

                    if [ "$DISK_USAGE" -ge 80 ]; then
                        echo "WARNING: Disk usage is high!"
                        exit 1
                    else
                        echo "Disk usage is healthy."
                    fi
                '''
            }
        }

        stage('Completed') {
            steps {
                echo "Pipeline executed successfully!"
            }
        }
    }
}
