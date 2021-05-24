pipeline {
    agent {
        docker {
            image 'qaninja/rubywd'
        }
    }
    
    stages {
        stage('Buid') {
            steps {
                echo 'Bulding or Resolve Depedenies!'
                sh 'rm -f Gemfile.lock'
                sh 'bundle install'
            }
        }
        stage ('Test') {
            steps {
                echo 'Executar testes em regressão'
                sh 'bundle exec cucumber -p ci'
                cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', jsonReportDirectory: 'logs', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
            }
        }
        stage('UAT'){
            steps {
                echo 'Aguarde até aceitação do usuário'
                input(message: 'Go to produção?', ok: 'Yes')
            }
        }
        stage ('Prod') {
            steps {
                echo 'WebApp is :)'
        }
    }
  }
}