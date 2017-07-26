# Docker Based Jenkins Build Agents Demo Configuration
This docker-compose config was used for the demonstration portion of the presentation at https://www.slideshare.net/EricSmalling1/docker-based-jenkins-build-agents-78280169
## Setup steps:

### Initial/pre-demo setup (do once)

**If using a Docker swarm:**
  * Run `docker stack deploy ci -c swarm.yml`
  * Run `docker service logs ci_jenkins` and copy the Jenkins admin token for the next step.

**If using docker-compose (non-swarm):**
  * Run `docker-compose up` and watch for the Jenkins admin token, copy it for next step.

---
### Beginning of demo
This is to show the audience that this is a stock install
_(If short on time, you can set this up in advance and begin demo at [Build demos](#builds) below)_
1. Point your browser at http://localhost , wait for Jenkins to ask for the admin token and paste in what you copied above.
1. Choose standard set of plugins
1. Skip admin user setup, and click "Start using Jenkins"
1. Go to http://localhost/computer/(master)/configure and change Usage to "Only build jobs with label...", click Save.
1. Go to http://localhost/configureSecurity/ and set "Access Control->Authorization" to "Anyone can do anything", click Save.
1. Go to http://localhost/pluginManager/available and select "Self-Organizing Swarm Plug-in Modules", click one of the "Install" options.
---
<a name="builds">
## Build demos
</a>
The intent is to create a few projects, all using Pipeline from Jenkinsfile files inside their repositories.
Feel free to use your own or the following 3 examples.

### Java/Maven Job setup
1. Click "Create New Jobs"
1. Give it a name, choose "Pipeline", click "OK"
1. Choose Pipeline->Definition: "Pipeline script from SCM"
  * SCM: Git
  * Repository URL: https://github.com/ericsmalling/mvn-web-sample.git
  * Click "Save"
1. Click "Build Now"

### JavaScript Job setup
1. Click "Create New Jobs"
1. Give it a name, choose "Pipeline", click "OK"
1. Choose Pipeline->Definition: "Pipeline script from SCM"
  * SCM: Git
  * Repository URL: https://github.com/ericsmalling/clarity.git
  * Click "Save"
1. Click "Build Now"

### GoLang Job setup
1. Click "Create New Jobs"
1. Give it a name, choose "Pipeline", click "OK"
1. Choose Pipeline->Definition: "Pipeline script from SCM"
  * SCM: Git
  * Repository URL: https://github.com/cloudbeers/multibranch-demo.git
  * Click "Save"
1. Click "Build Now"
---
## Optional executor-node scaling
If you feel the need, you can add additional executor-nodes via the following _(replace the '3' below with the count you want)_:
* **Swarm:**
  * `docker service scale ci_executor-node=3`
* **Non-Swarm:**
  * `docker-compose scale executor-node=3`
---
## Cleanup
When done, shut down the stack and optionally free up disk space:
* **Swarm:**
  * run `docker stack rm ci`
* **Non-Swarm:**
  * run `docker-compose stop;` (or just hit CTRL-C in the shell where you ran `docker-compose up`)
  * run `docker-compose rm`
* Run `rm -rf jenkins_home/* workspace/*` to remove the Jenkins server's home directory and executor workspaces.
