pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    sh 'printenv'
                    echo "Checking out code........"
                    def pullRequestBranch = env.GITHUB_PR_SOURCE_BRANCH ?: 'main'
                    checkout([$class: 'GitSCM', branches: [[name: "*/${pullRequestBranch}"]], userRemoteConfigs: [[url:'https://github.com/Zalman-Philip/users-app-server.git']]])
                    // Check if TAG_NAME exists
                    def TAG_NAME = sh(script: "git tag --contains ${env.GIT_COMMIT}", returnStdout: true).trim()
                    // Remove the leading "v" from the tag name
                    TAG_NAME = TAG_NAME.replaceAll(/^v/, '')
                    if (TAG_NAME) {
                        echo "GitHub Release Tag Name: ${TAG_NAME}"
                        // Add any other steps you need for when TAG_NAME exists
                    } else {
                        echo "No GitHub Release Tag found."
                        // Add any other steps you need for when TAG_NAME does not exist
                    }
                }
                script {
                    import groovy.json.JsonSlurper
                    echo 'getting request details'
                    try {
                        def requestBody = request.getReader().text
                        def headers = request.getHeaderNames()
                        headers.each { 
                          header -> 
                            println "$header: ${request."$header"}"
                        }
                        def jsonParser = new JsonSlurper()
                        def payload = jsonParser.parseText(requestBody)
                        println payload.action
                        echo 'success'
                    } catch (Exception e) {
                        echo 'Failed to get request details: ${e.message}'
                    }
                }
            }
        }
    }
}
