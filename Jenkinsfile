@NonCPS
def getLatestApprover(APPROVERS_GROUP) {
  def user = 'Anon'
  def approver = "False"
  // this returns a CopyOnWriteArrayList, safe for iteration
  def acts = currentBuild.rawBuild.getAllActions()
    for (act in acts) {
      if (act instanceof org.jenkinsci.plugins.workflow.support.steps.input.ApproverAction) {
        user = act.userId
        def groups = Jenkins.instance.securityRealm.loadUserByUsername(user).authorities
        for (group in groups) {
          if (group == APPROVERS_GROUP) {
            approver = "True"
          }
        }
      }
    }
    return [user, approver]
}

// A Function to allow pipelines to wait for an approved person/group to approve the next steps
