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
        sh 'ls -a;git --version'
        post
 stage 'Extra Check'
        sh 'pwd'
        echo 'from 55 second batch here is the change '
       }
 catch (e) {
    println '==================================================================================================='
    println 'since build is failed, rolling back to previous commit id'
    echo '==================================================================================================='
    sh '''
    a=$(git log -n 1 --skip 1 --pretty=format:%H)
    echo 'The previous commit id is "$a", Now we reverting to this commit id '
    git reset --hard $a
    git reset --soft HEAD@{1}
    git commit -m "Reverting to the state of the project at f414f31"
    git remote set-url origin "https://forpix:mdali%40786@github.com/forpix/Alto-Repo-Merge.git"
    git push origin HEAD:master
    '''
    currentBuild.result = 'UNSTABLE'             
       }        
      }
