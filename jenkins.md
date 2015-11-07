#Jenkins Continuous Integration  

Now that your project has been setup with a branching model and a versioning system, the next topic deals with automatically building and distributing the different branches and versions to team members. The sooner that quality engineers (QA), business analysts (BA) and product managers (PM) can get their hands on the latest version of the software, the faster that developers can get feedback on their work. [Jenkins](https://jenkins-ci.org) is a powerful and time-tested [Continuous Integration](https://en.wikipedia.org/wiki/Continuous_integration) system that provides this service.  

The project has been around since 2004 when it was developed by Sun Microsystems under the name Hudson and by way of a trademark dispute became known to the open-source community as Jenkins. Out-of-the-box Jenkins supports Subversion and CVS, and since Jenkins is extensible, there is a plugin to add [support for Git SCM](https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin).  

###Develop Branch  
A 'job' in Jenkins is the basic unit of continuous integration. A job can be used to build and/or merge multiple branches simultaneously. We will create one job specifically for the develop branch.

###Supporting Branches  
Now that the first Job for the project Git repository has been configured, it is easy to start creating more jobs for each branch. Instead of configuring additional jobs from scratch, the first job can be cloned and modified so that we only have to modify what we need.  

#####Release Branches  

#####Feature Branches  

#####Hotfix Branches  
