pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
    }
    stage("DeploytoStaging")
        when {
            branch 'master'
        }
    steps {
        withCredentials([usernamePassword(crenetialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
            sshPublisher(
                failOnError: false,
                continueOnError: true,
                publishers: [
                    sshPublisherDesc(
                        configName: 'staging',
                        sshCredentials: [
                            username: "$USERNAME",
                            encryptedPassprhase: "$USERPASS"
                            ],
                        transfers: [
                            sshTransfer(
                                sourceFiles: 'dist/trainSchedule.zip',
                                removePrefix: 'dist/',
                                remoteDirectory: '/root/jenkins-pipeline-build',
                                execCommand: 'sudo /usr/bin/systemctl stop train-schedule && rm -rf /opt/train-schedule/* && unzip /root/jenkins-pipeline-build/trainSchedule.zip -d /opt/train-schedule
                                }
                                }
                                                           

}
