def commitMessage = { sh(returnStdout: true, script: 'git log --format=%B --no-merges -n 1 || echo ""').trim() }
def isPullRequest = { env.CHANGE_ID != null ? "true" : "false" }

node {
	stage("Checkout") {
		checkout scm
	}

	stage('Preparation') {
		env.TRAVIS_COMMIT_MSG = commitMessage()
		env.TRAVIS_BRANCH = env.BRANCH_NAME
		env.TRAVIS_BETA_DEPLOY = TRAVIS_COMMIT_MSG.contains('[skip deploy]') ? 0 : 1
		env.TRAVIS_PULL_REQUEST = isPullRequest()
		env.SECRET1 = credentials('secret1')
		env.SECRET_FILE = credentials('abc1.txt')
	}
	
	stage('Build') {
		echo "Hi there! 1-2-3-"
		sh 'echo $SECRET1 – here'
		sh 'echo secret text - there'
		echo "--- ${TRAVIS_COMMIT_MSG} + ${TRAVIS_BRANCH} + ${TRAVIS_BETA_DEPLOY} + ${env.CHANGE_ID} %"
		sh 'echo ++ $TRAVIS_COMMIT_MSG ! $TRAVIS_BRANCH ! $TRAVIS_BETA_DEPLOY ! $CHANGE_ID %'
		
		echo "$SECRET_FILE"
		sh 'cp $SECRET_FILE ./secret'
		sh 'cat ./secret'
	}
}
