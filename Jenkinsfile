pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: "Maven-3.9.5", type: "maven"
    }

    stages {
        stage("CheckOutCodeGit") {
            steps {
                git 'https://github.com/Sivay3005/maven-web-application-obsqura.git'
                sh "ls"
            }
        }

        stage("Build") {
            steps {
                sh "${MAVEN_HOME}/bin/mvn clean package"
            }
        }

        stage("SonarQube") {
            steps {
                sh "${MAVEN_HOME}/bin/mvn clean sonar:sonar \
                    -Dsonar.projectKey=maven-web-application-obsqura \
                    -Dsonar.host.url=http://54.236.28.214:9000 \
                    -Dsonar.login=sqp_f06414594231f0e78dd3783544e85c9762b5afea"
            }
        }

        stage("UploadArtifactsintoNexus") {
            steps {
                sh "ls"
                sh "${MAVEN_HOME}/bin/mvn -s settings.xml deploy"
            }
        }

       
  }
}
