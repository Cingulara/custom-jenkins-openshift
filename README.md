# custom-jenkins-openshift
Customize the Jenkins S2I image to include plugins, k8s pod templates, etc.

## The plugins I want to include by default
* SonarQube
* Aqua Microscanner
* Slack - https://github.com/jenkinsci/slack-plugin
* Google Login - https://github.com/jenkinsci/google-login-plugin
* GitHub oAuth - https://github.com/jenkinsci/github-oauth-plugin
* Sonar Quality Gates - https://github.com/jenkinsci/sonar-quality-gates-plugin/blob/master/pom.xml
* Others

## Great reference point
https://github.com/godleon/openshift-jenkins-customization