// node{
//   stage( "Phase 1" ) {
//       checkout scm
//       def lastSuccessfulCommit = getLastSuccessfulCommit()
//       def currentCommit = commitHashForBuild( currentBuild.rawBuild.getCurrentBuild ) 
//       if (lastSuccessfulCommit) {
//         commits = sh(
//           script: "git rev-list $currentCommit \"^$lastSuccessfulCommit\"",
//           returnStdout: true
//         ).split('\n')
//         println "Commits are: $commits"
//     }
//   }
// }

// def getLastSuccessfulCommit() {
//   def lastSuccessfulHash = null
//   def lastSuccessfulBuild = currentBuild.rawBuild.getPreviousSuccessfulBuild()
//   if ( lastSuccessfulBuild ) {
//     lastSuccessfulHash = commitHashForBuild( lastSuccessfulBuild )
//   }
//   return lastSuccessfulHash
// }

// /**
//  * Gets the commit hash from a Jenkins build object, if any
//  */
// @NonCPS
// def commitHashForBuild( build ) {
//   def scmAction = build?.actions.find { action -> action instanceof jenkins.scm.api.SCMRevisionAction }
//   return scmAction?.revision?.hash
// }


// node{
//     passedBuilds = []

//     lastSuccessfulBuild(passedBuilds, currentBuild);

//     def changeLog = getChangeLog(passedBuilds)
//     echo "changeLog ${changeLog}"
// }

// def lastSuccessfulBuild(passedBuilds, build) {
//     if ((build != null) && (build.result != 'SUCCESS')) {
//         passedBuilds.add(build)
//         lastSuccessfulBuild(passedBuilds, build.getPreviousBuild())
//     }
// }

// @NonCPS
// def getChangeLog(passedBuilds) {
//     def log = ""
//     for (int x = 0; x < passedBuilds.size(); x++) {
//         def currentBuild = passedBuilds[x];
//         def changeLogSets = currentBuild.rawBuild.changeSets
//         for (int i = 0; i < changeLogSets.size(); i++) {
//             def entries = changeLogSets[i].items
//             for (int j = 0; j < entries.length; j++) {
//                 def entry = entries[j]
//                 log += "* ${entry.msg} by ${entry.author} \n"
//             }
//         }
//     }
//     return log;
// }

@Library('jenkins_example')_

stage ('Demo') {
    echo 'Hello world'
    sayHello 'Dave'
}

