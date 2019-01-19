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
* dotnetcore21JenkinsSlave - The Red Hat .NET Core 2.1 Jenkins Slave
* dotnetcore22JenkinsSlave - The Red Hat .NET Core 2.2 Jenkins Slave
* nodejs8JenkinsSlave - The Red Hat NodeJS 8 Jenkins Slave
* sonardotnetJenkinsSlave - a custom SonarQube Jenkins Slave with the dotnet sonarscanner global tool installed

You can add others by studying the structure and using the correct parameters and image references internal or external

## Adding Acccess to the Red Hat Docker Registry
If you have not already done so you need to setup a secret in OpenShift to pull from the RH Registry as it requires a Red Hat Developer account. The link is at the bottom of this page but the steps are really here. Perform them inside the "openshift" namespace specifically after you login with your OC command from the Username --> Copy Login Command in the top right corner of the OpenShift Web Console. Replace the "user-name" and "password" with your Red Hat Developer login and password. If you do not have one, go here: https://developers.redhat.com/.

```
oc project openshift

oc create secret docker-registry redhat-registry \
    --docker-server=registry.redhat.io \
    --docker-username=<user-name> \
    --docker-password=<password> \
    --docker-email=unused

oc secrets link default redhat-registry --for=pull

oc secrets link builder redhat-registry

oc create -f https://raw.githubusercontent.com/redhat-developer/s2i-dotnetcore/master/dotnet_imagestreams.json

oc replace -f https://raw.githubusercontent.com/redhat-developer/s2i-dotnetcore/master/dotnet_imagestreams.json
```

You may get warnings on the imagestreams. I ran both as I had to create a couple and update the rest. You can go to the OpenShift Web Console and then go to the openshift project and list the Build --> Images to ensure they are there.

## Great reference points that will help you
* https://github.com/godleon/openshift-jenkins-customization
* https://docs.openshift.com/container-platform/3.11/using_images/other_images/jenkins.html#jenkins-as-s2i-builder
* https://access.redhat.com/documentation/en-us/net_core/2.1/html/getting_started_guide/gs_dotnet_on_openshift