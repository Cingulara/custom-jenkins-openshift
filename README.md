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

## ConfigMaps for the K8s Pod Template setup in Jenkins within OpenShift
* baseJenkinsSlave - the CentOS7 base image used to run build commands and such
* dotnetcore22JenkinsSlave - The Red Hat .NET Core 2.2 Jenkins Slave
* nodejs8JenkinsSlave - The Red Hat NodeJS 8 Jenkins Slave
* sonardotnetJenkinsSlave - a custom SonarQube Jenkins Slave with the dotnet sonarscanner global tool installed

You can add others by studying the structure and using the correct parameters and image references internal or external

## Great reference points that will help you
* https://github.com/godleon/openshift-jenkins-customization
* https://docs.openshift.com/container-platform/3.11/using_images/other_images/jenkins.html#jenkins-as-s2i-builder