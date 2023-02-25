pipeline {
  agent any
  stages {
    stage('Install browser firefox') {
      steps {
        bat '''
          npx playwright install firefox
        '''
        bat '''
          npm i -D @playwright/test allure-playwright
        '''
      }
    }  
    stage('test') {
      steps {
        bat '''
        npx playwright test --project=firefox --reporter=line,allure-playwright
        '''
      }
    }
  }
    post('allure report'){
      always{
        script {
          allure([
        includeProperties: false, 
        jdk: 'JDK', 
        results: [[path: 'allure-results']]
        ])
      }
    }
      success{
        slackSend color: "bad", message: "https://mult.tv/iframes/2x2.php not seeing CORS error"
    }
  }
}