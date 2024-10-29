pipeline {
    parameters {
        choice choices: ['nodejs18', 'nodejs16', 'nodejs14'], description: 'Choose NodeJS version', name: 'NODEJS_TOOL_VERSION'
    }
    agent {
        kubernetes {
            label 'slave-2cpu-8gb'
        }
    }
    tools {
        nodejs params.NODEJS_TOOL_VERSION
    }
    stages {
        stage('Install Base Dependencies') {
            steps {
                cache(caches: [
                    arbitraryFileCache(
                        path: "node_modules",
                        includes: "**/*",
                        cacheValidityDecidingFile: "base-package.json"
                    )
                ]) {
                    // Install stable dependencies from package-stable.json
                    sh 'npm install'
                }
            }
        }
        stage('Install Dynamic Dependencies') {
            steps {
                // Install additional dependencies from main package.json
                sh 'npm install'
            }
        }
        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }
    }
}