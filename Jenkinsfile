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
                sshagent(['SSH_GITHUB']) {
                    sh 'echo $(date) > date.txt'
                    sh """  
                        export GIT_SSH_COMMAND="ssh -oStrictHostKeyChecking=no"
                        git remote set-url origin git@github.com:O5ten/kickass-recipes.git
                        git config --global user.email "ostberg.mikael@gmail.com"
                        git config --global user.name "Mikael Östberg"
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
