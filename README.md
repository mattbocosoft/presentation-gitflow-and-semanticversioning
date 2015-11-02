**CSCI 5828: Foundations of Software Engineering**  
*Fall 2015, Professor Kenneth Anderson*

Student: **Matthew Thomas**  
Presentation 3  

# Topics in Software Configuration Management  

Configuration Management is an important part of Software Engineering, and consists of many topics including source code management, build management, versioning and release management. This presentation will cover tools that help in these processes, and how they can applied in the context of mobile development.

Source code management
Build engineering
Environment configurations
Change control
Release engineering
Deployment

##Gitflow Branching Model  

![git-flow-extract-bw](images/git-flow-extract-bw.png)  

The Gitflow branching model was designed by [Vincent Driessen](http://nvie.com) and presented in his 2010 article ["successful Git branching model"](http://nvie.com/posts/a-successful-git-branching-model/). The article and Gitflow exploded in popularity and is now well-known and loved within the Git community.  

As the name suggests, Gitflow was created for use with the [Git source control management](https://git-scm.com) system. Gitflow could in theory be applied to most other forms of source control management. [Mercurial SCM](https://www.mercurial-scm.org) adapted an equivalent branching model called [Hg Flow](https://andy.mehalick.com/2011/12/24/an-introduction-to-hgflow/). However since Gitflow depends heavily on quick and lightweight branching so the cost of implementing Gitflow on another SCM would increase depending on how easy it is to branch.  

Developers who are accustomed to having a Configuration Management team in charge of the repository and branching are likely to find Git and Gitflow daunting, in part because branching is still viewed as a cumbersome and heavy process. Git branches are simply lightweight movable pointers in the repository, and they are quick to create and quick to be destroyed with no lasting consequences on the code-base. If a developer thinks that Gitflow is thus too complicated and overkill for a project, it's likely they need more exposure to Git and Gitflow documentation.  

###Tools  

As with Git, Gitflow can be implemented entirely from the command-line or via a user-interface. Here are two of the tools to bootstrap your Gitflow process.  

####Git Extensions  

Vincent Driessen also created a set of Git Extensions "to provide high-level repository operations" for Gitflow. These extensions can be found as an [open-source project on Github](https://github.com/nvie/gitflow) now supported by over 30 contributors.  

####SourceTree  

If you prefer to use a Graphical User-Interface (GUI), then [SourceTree](https://www.sourcetreeapp.com) is a good free option for OS X. It comes with [out-of-the-box support for both Gitflow and Hg Flow](http://blog.sourcetreeapp.com/2012/08/01/smart-branching-with-sourcetree-and-git-flow/).  

![sourcetree-gitflow](images/sourcetree-gitflow.png)  

###Usage  

The branches below describe the standard practices and naming conventions, although branches may be given different names if it's more clear for a team. For example, a team might call the develop branch 'trunk', or the master branch 'app-store'.  

###Master Branch  

After a release is deployed from either a release branch or a hotfix branch, the last commit should be merged into the master branch. Developers should never make direct commits on the master branch, rather each commit should result only from the merged from either a release or hotfix branch. After the merge, the merge-commit on the master branch is tagged with the version number using Semantic Versioning (see below).  

The master branch is a great way to be able to track and visualize the release history of a product in a single branch. The master branch also makes it easy to checkout the version of the code for a specific release.  

###Develop Branch  

In other branching models, this branch would be called the ['trunk'](https://en.wikipedia.org/wiki/Trunk_(software)), or 'main'. This is where the 'churn' happens, and contains the most up-to-date, though unstable, version of the code.  

A continuous integration job should be created to point to this branch, and should be built either with each commit or with a short time-interval such that QA can also have access to the latest build on this branch.

###Feature Branches  

*May branch off from: develop*  
*Must merge back into: develop*  
*Branch naming convention: feature/**  

New features should be developed on separate branches that spawn from the develop branch. These branches normally only reside on an individual developer's machine, but can be either shared with other developer's or pushed to the central repository if multiple developers are working on the same feature.  

After a feature is branched from develop and meanwhile a feature is being developed, other work will be being completed on the develop branch. Therefore in order to proactively resolve merge conflicts with the develop branch and harden the feature by integration testing, it is important to perform merges from the develop branch into the feature branch from time to time, especially if the feature branch in question is long-running. This concept is called 'Forward integration'. If the feature is a short branch, it is still a good idea to perform one reverse merge from develop to the feature branch before merging feature back into develop. In this way, smoke testing can  be performed on the isolated feature branch to make sure the feature development has not broken anything on the develop branch. When testing is complete, the feature can be merged without any conflicts back into the develop branch.  

A powerful benefit of keeping feature development on separate branches, is the ability to elevate the Agile value of flexibility over following a plan. When a release branch is created, only those features that have been merged into develop will be included into the release. That way, there will not be any unfinished feature work holding up the release. The develop branch will always be ready for a release branch to be created.  

If the branch is long-running, then a continuous integration job can be created to point to the feature branch so that QA can proactively work with developers to solidify the feature before merging into develop.  

###Release Branches  

*May branch off from: develop*  
*Must merge back into: develop and master*  
*Branch naming convention: release/X.Y.Z*  

Gitflow works best on an Agile team where releases and versioning are flexible and value is placed on "responding to change over following a plan". In Gitflow, releases are not assigned a version (e.g. X.Y.Z) until code-complete. This flows well with teams who think about a release in terms of the new features or bug fixes that the release comprised of, rather than teams that commonly talk about releases more abstractly by their version. As [Kent Beck](https://en.wikipedia.org/wiki/Kent_Beck) creator of Extreme Programming (XP) recommends, Agile teams should think about releases in terms of "themes", functionality for each release that has been specified at a high level. This also encourages all product members, not just developers, to be more aware of the current features in development. It's easy to get out-of-touch with a product, its features, and the value being delivered to users when the team depends too heavily on version numbers. Additionally, when version numbers change, like in the case of hotfixes, a team that depends on version numbers will have to scramble to readjust their release plan whereas a team using release themes will not be affected.  

A separate continuous integration job should be created for each release branch so that QA can test changes made before deployment.  

###Hotfix Branches  

*May branch off from: master*  
*Must merge back into: master and (release or develop)*  
*Branch naming convention: hotfix/X.Y.Z*  

I talked earlier about thinking about releases in terms of "themes" instead of versions. Hotfixes are one reason why this might be important. Hotfixes are unplanned and urgent changes that do not fit into the scheduled release plan, therefore they would disrupt and offset any planned versions. An obvious resolution for this would be to add a hotfix component to the version number; i.e. Major.Minor.Patch.*Hotfix* however this would break from the Semantic Versioning standard practices.  

The process for a hotfix is as follows:  
1. Client reports critical and urgent issue.  
2. Hotfix branch created from the master branch.  
3. One or two commits are created on the new hotfix branch.  
4. QA tests the commits from builds pointing directly at the hotfix branch.  
5. Development and testing are complete, so deploy latest hotfix commit.  
*After successful deployment...*  
6. Merge hotfix branch into master branch, and tag commit on master branch with version number.  
7a. If a release is in progress, merge hotfix into release branch.  
7b. Else, merge hotfix branch into develop branch.  

A separate continuous integration job should be created for each release branch so that QA can test changes made before deployment.  

###Tagging  

Tagging should be used to identify release versions on the master branch and should use the Semantic Versioning conventions. Tagging can also be used to mark an early-adopter build that was sent to the client from the develop branch or a feature branch.  

If the git repository is using submodules, tagging does not necessarily need to be used on the submodules because the tagged commits the parent repository will by definition point to the correct commits in the submodules.  

###Strategies for App Store Updates  

Both the Apple App Store and Google Play stores now use a review process to vet app updates for security concerns, UI/UX convention violations, and stability. It is recommended not to merge from release or hotfix into the master branch until the release or hotfix is approved. However, in order to keep the develop branch up-to-date meanwhile the release is going through the review process, the release or hotfix branch can be merged back into develop even before the review takes place. That way, the repository will also contain a record of how many times a given release or hotfix was submitted for review before it was approved.  

###References  

[A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)  
[A short introduction to Git Flow (Video)](https://vimeo.com/16018419)  
[Using git-flow to automate your git branching workflow](http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/)  

##Semantic Versioning  

![semantic-versioning](images/semantic-versioning.png)  

Semantic Versioning is an attempt to, as it's name suggests, standardize the *meaning* as well as syntax of version numbers. The [main webpage of the Semantic Versioning project](http://semver.org) declares that the goal of the project is to deal with 'dependency hell'. Indeed, Semantic Versioning is a very popular versioning convention adopted by [CocoaPods](https://github.com/mattbocosoft/presentation-cocoapods) and allows product developers to be able to count on the backwards-compatibility of dependency updates.  

Semantic Versioning formalizes the versioning system that many products already use in an informal way. Organizations often increment the major number when the change 'feels' big, or the minor number when the change 'feels' minor, however this methodology is not exact; "Without compliance to some sort of formal specification, version numbers are essentially useless for dependency management". [Not everyone agrees](https://gist.github.com/jashkenas/cbd2b088e20279ae2c8e) with the practice of Semantic Versioning, arguing that Semantic Versioning "prioritize[s] a mechanistic understanding of a codebase over a human one".  

There are many unique methods of assigning versions to product releases, and each organization has it's own unique style. Here are some example  
1. OS X: Apple uses a two-component version number (e.g. 10.11) combined with a natural language name (e.g. "El Capitan").  
2. iOS uses a three-component version number much like Semantic Versioning, and may in fact be *using* Semantic Versioning    
3. Android uses [three different versions](https://en.wikipedia.org/wiki/Android_version_history) for each release, e.g. 4.4–4.4.4 Android KitKat (API level 19)  

###Beginning Development  

The initial version of a product or library using Semantic Versioning starts at 0.1.0. Since all changes are potentially break backwards-compatibility, it does make sense to increase the major version until release, so the product does not increase to 1.0.0 until the first public release. If the software is already in use, then the version number should already be at or above 1.0.0  

###Major  
The Major number should be incremented when backward-*incompatible* functionality is introduced in the release. This indicates to the consumers of the software or library that they need to be prepared to change their integration methods with the software or library.  

The release that corresponds to an increment in the major version may also include changes that are minor or patch level.  

The Minor and Patch numbers must be reset to 0 when the Minor number is incremented.  

###Minor  
The Minor number should be incremented when new backwards-compatible functionality is introduced in the release. This indicates to consumers of the software or library that they can safely upgrade to the latest Minor release without having to worry about backwards-compatibility issues.  

The release that corresponds to an increment in the minor version may also include changes that are patch level, but not major level.  

The Patch number must be reset to 0 when the Minor number is incremented.  

###Patch  
The Patch number should be incremented when backwards-compatible bug-fixes is introduced in the release. This indicates to consumers of the software or library that they can safely upgrade to the latest Patch release without having to worry about backwards-compatibility issues.  

###Pre-Release  
Pre-release numbers are appended after the Patch number following a dash. They can include any number of components separated by a dot. An example of a version with a pre-release number is 1.4.2-beta.2  

###References  
[http://semver.org](http://semver.org)  

##Fastlane.tools  
