# release-project

## Working in Continuous Integration

In a continuous integration environment like Jenkins or Hudson, 
you don't want to have an interactive release process. 
To avoid having to enter any information manually during the process, 
you can tell the plugin to automatically set and update the version number.

You can do this by setting the ***release.useAutomaticVersion*** property on the command line, 
or in Jenkins when you execute gradle. The version to release and the next version can be optionally 
defined using the properties ***release.releaseVersion*** and ***release.newVersion***.

> gradle release -Prelease.useAutomaticVersion=true -Prelease.releaseVersion=1.0.0 -Prelease.newVersion=1.1.0-SNAPSHOT



## Useful links 

- How to write tasks with gradle:
> https://docs.gradle.org/current/userguide/tutorial_using_tasks.html#N102B2

- MD file syntax:
> https://www.markdownguide.org/basic-syntax/

