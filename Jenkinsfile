pipeline {
      agent any
      stages {
          stage('One') {
          steps {
            echo 'Begin of Pipeline: Stage one completes'
          }
          }
          stage('Two') {
          steps {
            input('Do you want to update to Development container?')
          }
          }
          stage('Three') {
          when {
                not {
                    branch "Development NOT updated"
                }
          }
          steps {
                 sh '''#!/bin/bash
                 docker exec -it puppetclient1 /bin/bash;
                 cd /testdir/clone;
                 git clone https://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@github.com/daemianKoh/devops_repo.git
                 locate_script='/testdir/clone/script_to_run';
                 bolt script run $locate_script -t $targets -u clientadm -p user123 --no-host-key-check --run-as root;
                 '''
                 echo "Development container updated"
          }
          }
          stage('Four') {
          steps {
            input('Do you want to update to Production container: Proceed to Production')
                
          }
          }
          stage('Five') {
          when {
                not {
                    branch "Production NOT updated"
                }
          }
          steps {
                 sh '''#!/bin/bash
                 targets=puppetclient2;
                 cd /testdir/clone;
                 git clone https://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@github.com/daemianKoh/devops_repo.git
                 locate_script='/testdir/clone/script_to_run';
                 bolt script run $locate_script -t $targets -u clientadm -p user123 --no-host-key-check --run-as root;
                 '''
                 echo "Production container updated"
          }
          }
          stage('Completed updating Operation') {
          steps {
            echo 'Completed updating to Production Container'
          }
          }
      }
}
