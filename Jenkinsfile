node('master') 
    {
        stage('continues download') 
        {
            git 'https://github.com/imranks2329/tomcat-jenkins-deploy.git'
        }
        stage('continues build') 
        {
            sh 'mvn package'
        }
        stage('continues archive to artifacts') 
        {
            archiveArtifacts artifacts: '**/webimran.war', followSymlinks: false
        }
        stage('deploy to test env') 
        {
            deploy adapters: [tomcat8(credentialsId: '99559bf4-f22e-436a-80c0-3e1c6b42ce8a', path: '', url: 'http://192.168.43.128:9090/')], contextPath: '/', war: '**/*.war'
        }
        stage('deploy to test prod') 
        {
            timeout(time: 5, unit: 'DAYS') {
        input 'Approve PRODUCTION Deployment?'
        }
            deploy adapters: [tomcat8(credentialsId: '99559bf4-f22e-436a-80c0-3e1c6b42ce8a', path: '', url: 'http://192.168.43.55:9090/')], contextPath: '/', war: '**/*.war'  
        }
    }   

