pipeline {
  agent any
  stages {
    stage('uninstall all') {
      parallel {
        stage('uninstall all') {
          steps {
            sh 'echo "uninstall";'
          }
        }
        stage('rm composer.lock') {
          steps {
            sh '#rm composer.lock'
          }
        }
      }
    }
    stage('clean install') {
      steps {
        sh '''cp .env.example .env
composer install
php artisan config:clear
php artisan cache:clear
#php artisan route:clear
php artisan view:clear
#php artisan optimize
php artisan key:generate
#php artisan migrate:install
#php artisan db:seed
'''
      }
    }
    stage('testing') {
      steps {
        sh 'phpunit'
      }
    }
    stage('building js') {
      parallel {
        stage('building php') {
          steps {
            sh '''composer install --optimize-autoloader --no-dev
php artisan config:cache
'''
          }
        }
        stage('build js') {
          steps {
            sh '''npm install
npm run production'''
          }
        }
      }
    }
    stage('create zip') {
      steps {
        sh 'echo "zip";'
      }
    }
  }
}