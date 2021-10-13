pipeline {
  agent any
  environment {
    APP_NAME = 'test'
  }
  options {
    // Stop the build early in case of compile or test failures
    skipStagesAfterUnstable()
  }
  stages {

    stage('Detect build type') {
      steps {
        script {
          if (env.BRANCH_NAME == 'master' || env.CHANGE_TARGET == 'master') {
            env.BUILD_TYPE = 'release'
          } else {
            env.BUILD_TYPE = 'debug'
          }
        }
      }
    }

    stage('Compile') {
      steps {
        // Compile the app and its dependencies
        sh './gradlew compile${BUILD_TYPE}Sources'
      }
    }

    stage('Build') {
      steps {
        // Compile the app and its dependencies
        sh './gradlew assemble${BUILD_TYPE}'
      }
    }

    stage("Lint") {
        steps {
            sh './gradlew lint'
        }
    }

//     stage('Publish') {
//       steps {
//         // Archive the APKs so that they can be downloaded from Jenkins
//         archiveArtifacts "**/assets/build/*.apk"
//         // Archive the ARR and POM so that they can be downloaded from Jenkins
//         // archiveArtifacts "**/${APP_NAME}-${BUILD_TYPE}.aar, **/*pom-   default.xml*"
//       }
//     }

  }
}