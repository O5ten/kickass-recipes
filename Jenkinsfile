pipeline {
   agent {
       label 'foxtrot'
   }
   stages {
       stage('Clone'){
           steps {
               git url: 'git@github.com:O5ten/kickass-recipes.git', credentialsId: 'SSH_GITHUB', branch: 'master'
           }
       }       
       stage(''){
           steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'SSH_GITHUB', keyFileVariable: 'key')]) {
                    sh 'echo $(date) > date.txt'
                    sh """  
                        git remote set-url origin git@github.com:vidispine/vidispine-python-sdk.git
                        git config core.sshCommand 'ssh -i $key'
                        git checkout develop
                        git add date.txt
                        git commit -m "Update date"
                        git push origin develop
                    """
                }
           }
       }
   }
}
