def commitMessage() {
	return sh(returnStdout: true, script: "git log --format=%B --no-merges -n 1").trim()
}

pipeline {
	agent any
	environment {
		TRAVIS_COMMIT_MSG = commitMessage()
		TRAVIS_BRANCH = "${BRANCH_NAME}"
		TRAVIS_BETA_DEPLOY = "${TRAVIS_COMMIT_MSG.contains('[skip deploy]') ? 0 : 1}"
	}
	stages {
		stage("Prepare") {
			steps {
				echo "${TRAVIS_COMMIT_MSG} + ${TRAVIS_BRANCH} + ${TRAVIS_BETA_DEPLOY}"
				sh 'echo $TRAVIS_COMMIT_MSG ! $TRAVIS_BRANCH ! $TRAVIS_BETA_DEPLOY'
			}
		}
	}
}
