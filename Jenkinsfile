#!/usr/bin/env groovy
/*
 *    This for comment section only !
 *    
 */
import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurperClassic
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import java.net.URL

node('master') {
       try{
       
stage '\u2756  git checkout scm'
     cleanWs() 
        echo'__________________________________________________________________________________________________________________'
        def scmVars = checkout scm
        echo'___________________________________________________________________________________________________________________'
        echo 'scm : the commit id is ' +scmVars.GIT_COMMIT
        echo 'scm : the commit branch  is ' +scmVars.GIT_BRANCH
        echo 'scm : the previous commit id is ' +scmVars.GIT_PREVIOUS_COMMIT
       sh 'ls -a'
       sh '''
       git log --oneline -1 ${GIT_COMMIT} 
       git log --format="medium" -1 ${GIT_COMMIT} 
       git name-rev --name-only HEAD
       '''
       echo '========= ================== ================== =============== =========== = ===================='
       def commitBranch = sh(returnStdout: true, script: "git name-rev --name-only HEAD")
       echo " branch name  is'${commitBranch}'"
       sh '''
       git_branch_local=$(echo $GIT_BRANCH   | sed -e "s|origin/||g")
       echo GIT_BRANCH_LOCAL=$git_branch_local > build.properties
       '''
       }
       catch {
           sh '''
          a=$(git log -n 1 --skip 1 --pretty=format:%H)
          echo 'The previous commit id is $a, Now we reverting to this commit id '
          git revert $a
         git remote set-url origin "https://forpix:mdali%40786@github.com/forpix/Alto-Repo-Merge.git"
         git push origin --tags
          
          '''
         currentBuild.result = 'UNSTABLE'      
       }
       
                
      }
