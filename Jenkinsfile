pipeline {
    agent {
        kubernetes {
            label 'slave-4cpu-16gb'
        }
    }
    stages {
        stage('Restore npm Cache') {
            steps {
                cache(caches: [
                    arbitraryFileCache(
                        path: "node_modules",
                        includes: "**/*",
                        cacheValidityDecidingFile: "package-lock.json"
                    )
                ]) {
                    sh 'npm install'
                }
            }
        }
        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }
    }
}