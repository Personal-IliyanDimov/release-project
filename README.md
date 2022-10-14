# release-project

## Multi-Project Builds

Support for multi-project builds isn't complete, but will work given some assumptions. 
The gradle-release plugin assumes and expects that only one version control system is used by both root and sub projects.

Apply the plugin separately to each subproject that you wish to release. Release using a qualified task name, e.g.:
> ./gradlew :sub:release # release a subproject named "sub"

> ./gradlew :release # release the root project

## Working in Continuous Integration

In a continuous integration environment like Jenkins or Hudson, 
you don't want to have an interactive release process. 
To avoid having to enter any information manually during the process, 
you can tell the plugin to automatically set and update the version number.

- Option 1: Override version in gradle.properties file via parameters:

> You can do this by setting the ***release.useAutomaticVersion*** property on the command line, 
> or in Jenkins when you execute gradle. The version to release and the next version can be optionally 
> defined using the properties ***release.releaseVersion*** and ***release.newVersion***.
> 
>> gradle release -Prelease.useAutomaticVersion=true -Prelease.releaseVersion=1.0.0 -Prelease.newVersion=1.1.0-SNAPSHOT

- Option 2: Use the version in gradle.properties to do automatic versioning

> Uses the version in gradle.properties to do the release and then increments it.
> By default increments the last digit of the version only so if you like to override do it before the release procedure.
> 
>> gradle release -Prelease.useAutomaticVersion=true


## Useful links 

- How to write tasks with gradle:
> https://docs.gradle.org/current/userguide/tutorial_using_tasks.html#N102B2

- MD file syntax:
> https://www.markdownguide.org/basic-syntax/

- Remove tags:
> git push --delete origin <tag e.g 0.0.1>

- List tags:
> git tag 

- List remote tags:
> git ls-remote --tags origin

