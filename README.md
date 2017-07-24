Setup steps:

## Initial setup (do once)
1. Run `docker stack deploy ci -c docker-compose.yml`
1. Point your browser at http://localhost , wait for Jenkins to ask for the admin token.
1. Run `docker service logs ci_jenkins` and copy the token, paste it into Jenkins web UI
1. Choose standard set of plugins
1. Skip admin user setup, and click "Start using Jenkins"
1. Go to http://localhost/computer/(master)/configure and change Usage to "Only build jobs with label...", click Save.
1. Go to http://localhost/configureSecurity/ and set "Access Control->Authorization" to "Anyone can do anything", click Save.
1. Go to http://localhost/pluginManager/available and select "Self-Organizing Swarm Plug-in Modules", click one of the "Install" options.
1. Start tailing executor-node logs using `docker service logs -f ci_executor-node` and wait for all to connect, verify it in the Jenkins web UI

## Java/Maven Job setup
1. Click "Create New Jobs"
1. Give it a name, choose "Pipeline", click "OK"
1. Choose Pipeline->Definition: "Pipeline script from SCM"
  * SCM: Git
  * Repository URL: https://github.com/ericsmalling/mvn-web-sample.git
  * Click "Save"
1. Click "Build Now"

## JavaScript Job setup
1. Click "Create New Jobs"
1. Give it a name, choose "Pipeline", click "OK"
1. Choose Pipeline->Definition: "Pipeline script from SCM"
  * SCM: Git
  * Repository URL: https://github.com/ericsmalling/clarity.git
  * Click "Save"
1. Click "Build Now"

## GoLang Job setup
1. Click "Create New Jobs"
1. Give it a name, choose "Pipeline", click "OK"
1. Choose Pipeline->Definition: "Pipeline script from SCM"
  * SCM: Git
  * Repository URL: https://github.com/cloudbeers/multibranch-demo.git
  * Click "Save"
1. Click "Build Now"
