pipeline { 
  agent any
   tools { 
    gradle "Gradle"
  }
  stages { 
    stage('Clone Repository') {
      steps { 
        git credentialsId: 'my-ssh-credentials', url: 'git@github.com:Ramayan0/java-todo.git'
      }
    }
    stage('Build project') {
        steps { 
            sh 'gradle build'
        }
    }
    stage('Tests') {
        steps { 
            sh 'gradle test'
            
        }
        
    }
    stage('Check Remotes') {
  steps {
    sh 'git remote -v'
  }
}
stage('Remove Existing Remote') {
  steps {
    sh 'git remote remove heroku || true'  // || true ensures no error if the remote doesn't exist
  }
}

    stage('Deploy to Heroku') {
  steps {
    withCredentials([usernamePassword(credentialsId: 'heroku', passwordVariable: 'HEROKU_API_KEY', usernameVariable: 'HEROKU_USER')]) {
      sh '''
        git remote add heroku https://$HEROKU_USER:$HEROKU_API_KEY@git.heroku.com/calm-fortress-08149.git
        git push heroku master
      '''
    }
  }
}

  }
}
