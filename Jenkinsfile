pipeline {
   agent {
       label 'master'
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
                        git remote set-url origin git@github.com:O5ten/kickass-recipes.git
                        git config core.sshCommand 'ssh -i $key'
                        git fetch origin master
                        git checkout master
                        git add date.txt
                        git commit -m "Update date"
                        git push origin master
                    """
                }
           }
       }
   }
}
