# Development flow by manual(start from v1.0.0-SNAPSHOT)
## Step 1 - Development on current snapshot version
## Step 2 - Deploy current snapshot version(Many times)
- mvn deploy -s ./settings.xml -Drepo.id=nexus-snapshots -Drepo.user=admin -Drepo.pass=123456
## Step 3 - Release current snapshot version(One time)
- Change pom version to v1.0.0(commit)
- mvn deploy -s ./settings.xml -Drepo.id=nexus-releases -Drepo.user=admin -Drepo.pass=123456
- git tag v1.0.0
- git push origin v1.0.0 / git push --tags
## Step 4 - Start next snapshot version
- Change pom version to v1.0.1-SNAPSHOT(commit)


# Development flow by release plugin(start from v1.0.1-SNAPSHOT)
## Step 1 - Development on current snapshot version
## Step 2 - Deploy current snapshot version(Many times)
- mvn deploy -s ./settings.xml -Drepo.id=nexus-snapshots -Drepo.user=admin -Drepo.pass=123456
## Step 3 - Release current snapshot version and start next snapshot version
- mvn release:prepare
- mvn release:perform -s ./settings.xml -Drepo.id=nexus-releases -Drepo.user=admin -Drepo.pass=123456


# Apache Maven Deploy Plugin 用法
## deploy:deploy - Deploy maven project(pom.xml, settings.xml)
- pom.xml(distributionManagement<repository, snapshotRepository>) - Config repository Info(repositoryId, url)
- settings.xml(Servers<Server>) - Config auth(repositoryId, username, password) info for repository
- mvn deploy [-s <setting file>]
## deploy:deploy-file - Deploy　file　by　command
- settings.xml(Servers<Server>) - Config auth(repositoryId, username, password) info for repository
- mvn deploy:deploy-file [-s <setting file>] -Dfile=<file> -DrepositoryId=<repositoryId> -Durl=<url of repository> -DgroupId=<group> -DartifactId=<artifact> -Dversion=<version> -Dpackaging=jar
- mvn deploy:deploy-file [-s <setting file>] -Dfile=<file> -DrepositoryId=<repositoryId> -Durl=<url of repository> -DpomFile=<pom file for get group, artifact, version and package info>