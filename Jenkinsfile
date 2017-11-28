def commitMessage = { sh(returnStdout: true, script: 'git log --format=%B --no-merges -n 1 || echo ""').trim() }

node {
	stage("Checkout") {
		checkout scm
	}

	stage('Preparation') {
		env.TRAVIS_COMMIT_MSG = commitMessage()
		env.TRAVIS_BRANCH = env.BRANCH_NAME
		env.TRAVIS_BETA_DEPLOY = TRAVIS_COMMIT_MSG.contains('[skip deploy]') ? 0 : 1
	}
	
	stage('Build') {
		echo "--- ${TRAVIS_COMMIT_MSG} + ${TRAVIS_BRANCH} + ${TRAVIS_BETA_DEPLOY} + ${env.CHANGE_ID} %"
		sh 'echo ++ $TRAVIS_COMMIT_MSG ! $TRAVIS_BRANCH ! $TRAVIS_BETA_DEPLOY ! $CHANGE_ID %'
	}
}
