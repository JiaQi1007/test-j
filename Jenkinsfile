void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/tardisone/bass-ats.git"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ])
}

pipeline {
    agent any
    stages {
        stage('pretreatment') {
            steps {
                setBuildStatus('Building','PENDING')
                echo '------------------------------\n' +
                        '         pretreatment          ' +
                        '\n------------------------------'
            }
        }
    }
    post {
        always {
            setBuildStatus("Build succeeded", "SUCCESS")
        }
        success {
            setBuildStatus("Build succeeded", "SUCCESS")
        }
        failure {
            setBuildStatus("Build failed", "FAILURE")
        }
    }
}
