node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --prefer-dist --no-dev --ignore-platform-reqs'
        sh 'php artisan config:cache'
        // sh 'php artisan route:cache'
    }
    
    stage('Config'){
        parallel(
            'config cahe':{
                sh 'php artisan config:cache'
            },
            'config route':{
                sh 'php artisan route:cache'
            }
        )
    }
    
    stage('Docker Build') {
        sh 'docker build -t ruansvictor/todoapi:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push ruansvictor/todoapi:$BUILD_NUMBER'
    }
}
