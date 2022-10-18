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


## Rules to follow for Gitflow 


Gitflow Workflow

Gitflow is a legacy Git workflow that was originally a disruptive 
and novel strategy for managing Git branches. 

Gitflow has fallen in popularity in favor of trunk-based workflows, 
which are now considered best practices for modern continuous software development and DevOps practices. 

Gitflow also can be challenging to use with CI/CD. This post details Gitflow for historical purposes.

### The overall flow of Gitflow 
Rules: 
1. A ***develop*** branch is created from ***main*** 
2. A ***release*** branch is created from ***develop*** 
3. ***feature*** branches are created from ***develop*** 
4. When a ***feature*** is complete it is merged into the ***develop*** branch 
5. When the ***release*** branch is done it is merged into ***tag*** 
6. If an issue in ***main*** is detected a ***hotfix*** branch is created from ***main***    
7. Once the ***hotfix*** is complete it is merged to both ***develop*** and ***main***

Additional rules:
- If and only if ***feature*** branch is created from ***develop*** it should be merged back to it (affects rule 3 and 4)
- ***develop*** branch is used for active development of one and only one latest version (affects rule 5)
- if multiple releases (release-1.0, release-2.0) are developed in parallel then features are created from corresponding branch (affects rule 3)
- ***hotfix*** might be merged to ***release*** branches if it affects them (affects rule 7)

## Rules to follow for Trunk based strategies 

Looks like bullshit to me. 

Might be used only by teams that are build from developers with very big experience 
(at least senior with 5-7 years experience).



## Useful links 

- How to write tasks with gradle:
> https://docs.gradle.org/current/userguide/tutorial_using_tasks.html#N102B2

- MD file syntax:
> https://www.markdownguide.org/basic-syntax/

- Gitflow:
> https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

- Trunk based development
> https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development

## Commands 

- Remove tags:
> git push --delete origin <tag e.g 0.0.1>

- List tags:
> git tag 

- List remote tags:
> git ls-remote --tags origin

- Check tags associate with branches
> ubuntu@ubuntu2004:~/GitHub/release-project$ git tag
>> 0.0.1,
>> 0.0.2,
>> 0.0.3,
>> 1.0.0,
>> 1.1.0,
>> 1.1.1,
>> 1.1.2,
>> 1.1.3,
>> 1.1.4
> 
> ubuntu@ubuntu2004:~/GitHub/release-project$ git branch --contains 1.1.4
>> release-v1
> 
> ubuntu@ubuntu2004:~/GitHub/release-project$ git branch --contains 1.1.3
>> release-v1
> 
> ubuntu@ubuntu2004:~/GitHub/release-project$ git branch --contains 0.0.1
> 
> develop,
> main,
> release-v1

