node{
    stage('code checkout'){
        git 'https://github.com/Nachiket-01/capstone-project-demo.git'
    }


    
    stage('build'){
      sh 'mvn clean package'  
    }
    
    stage('package as docker image'){
      sh 'docker build -t nachikets01/insure-me:1.0 .'
    }
    
    stage('push to dockerhub'){
        
    withCredentials([string(credentialsId: 'DockerPass', variable: 'DockerPass')]) {
    sh "docker login -u nachikets01 -p ${DockerPass}"
    sh 'docker push nachikets01/insure-me:1.0'
    }
    }
    
    stage('deploy to test-environment') {
        ansiblePlaybook credentialsId: '9dcad404-c947-420c-b948-0685b6ece62f', disableHostKeyChecking: true, inventory: '/etc/ansible/hosts', playbook: 'deploy-prod-server.yml', vaultTmpPath: ''
        
        
    }
    
    
    
}
