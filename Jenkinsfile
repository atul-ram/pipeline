node {
   
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Login', url: 'http://root@worker5.local/root/pipeline-01.git']]])
     
   }
   stage('Check') { // for display purposes
      //syntax check
      ansiblePlaybook colorized: true, credentialsId: 'ansible-user', extras: '--syntax-check', inventory: 'inventory', playbook: 'ping.yml', sudoUser: null
      
   }
   stage('Execute') { // for display purposes
      //execute playbook

      try {
      ansiblePlaybook colorized: true, credentialsId: 'ansible-user', inventory: 'inventory', playbook: 'ping.yml', sudoUser: null
     }catch(e){
	       // if any exception occurs, mark the build as failed
            currentBuild.result = 'FAILURE'
            throw e
        } finally {
            // perform workspace cleanup only if the build have passed
            // if the build has failed, the workspace will be kept
           deleteDir()
       }
      
   }
   }
