#!groovy

// A Declarative Pipeline is defined within a 'pipeline' block.
pipeline {

  // agent defines where the pipeline will run.
  agent {
    label ""
  }
  
//  tools {
    // pipeline level tools
//  }
  
  environment {
    FOO = "BAR"
  }
  
  stages {
    stage("first stage") {
      steps {
        echo "Foo is ${env.FOO}"
      }
      
      // Post can be used both on individual stages and for the entire build.
      post {
        success {
          echo "Only when we haven't failed running the first stage"
        }
        
        failure {
          echo "Only when we fail running the first stage."
        }
      }
    }
    
    stage('second stage') {
//      tools {
        // overriding environment and agent tools settings
//      }
      
      steps {
        echo "second stage step"
      }
    }
    
    stage('third stage') {
      steps {
        parallel(one: {
                  echo "I'm on the first branch!"
                 },
                 two: {
                   echo "I'm on the second branch!"
                 },
                 three: {
                   echo "I'm on the third branch!"
                   echo "But you probably guessed that already."
                 })
      }
    }
  }
  
  post {
    // Always runs. And it runs before any of the other post conditions.
    always {
      // Let's wipe out the workspace before we finish!
      deleteDir()
    }
    
    success {
      echo "DONE!"
    }
  }
  
  // The options directive is for configuration that applies to the whole job.
  options {
    // For example, we'd like to make sure we only keep 10 builds at a time, so
    // we don't fill up our storage!
    buildDiscarder(logRotator(numToKeepStr:'3'))
    
    // And we'd really like to be sure that this build doesn't hang forever, so
    // let's time it out after an hour.
    timeout(time: 60, unit: 'MINUTES')
  }

}
