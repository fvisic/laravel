pipeline {
  agent any
  stages {
    stage('uninstall all') {
      steps {
        sh 'echo "uninstall";'
      }
    }
    stage('clean install') {
      steps {
        sh '''cp .env_example .evn
composer install
php artisan config:clear
php artisan cache:clear
php artisan route:clear
php artisan view:clear
php artisan optimize
php artisan key:generate
php artisan migrate:install
php artisan db:seed
'''
      }
    }
    stage('testing') {
      steps {
        sh 'phpunit test'
      }
    }
  }
}