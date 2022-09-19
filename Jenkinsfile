pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                sh 'git clone git@github.com:gummallasainathreddy/simple-java-maven-app.git'
            }
        }
         stage('package') {
            steps {
                sh '/opt/maven3/bin/mvn clean package'
            }
        }
         stage('upload to artifactory') {
            steps {
                sh 'mv target/my-app-1.0-SNAPSHOT.jar my-app-$BUILD_NUMBER.jar'
                sh 'aws s3 cp my-app-$BUILD_NUMBER.jar s3://artifactory-sainath/'
            }
        }
          stage('download from artifactory') {
            steps {
                sh 'aws s3 cp  s3://artifactory-sainath/my-app-$BUILD_NUMBER.jar .'

            }
        }
           stage('deploy on targets') {
            steps {
                sh 'scp my-app-$BUILD_NUMBER.jar root@172.31.37.240:/opt/tomcat9/webapps'
            }
        }


    }
}
