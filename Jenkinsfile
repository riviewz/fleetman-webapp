node {
   stage('Prepare') {
      git 'https://github.com/riviewz/fleetman-webapp'
   }
   stage('Build') {
      sh "mvn clean package"
   }
   stage('Results') {
      archive 'target/*.war'
   }
   stage('Deploy') {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_user', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
			ansiblePlaybook becomeUser: null, credentialsId: 'ssh_user', disableHostKeyChecking: true, installation: 'ansible_install_dir', playbook: 'deploy.yaml', sudoUser: null
		}         
   }   
}
