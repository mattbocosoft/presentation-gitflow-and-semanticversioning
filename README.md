**CSCI 5828: Foundations of Software Engineering**  
*Fall 2015, Professor Kenneth Anderson*

Student: **Matthew Thomas**  
Presentation 3  

# Topics in Software Configuration Management  

Configuration Management is an important part of Software Engineering, and consists of many topics including source code management, build management, versioning and release management. This presentation will cover two of the most popular tools that support these processes within the context of Agile software development. I will draw from my personal experience with [developing mobile software](https://github.com/mattbocosoft/presentation-xcode) both in the context of small personal projects and large-scale multi-team projects, and show how these tools help at both scales.  

The tools below have been chosen because they support the values laid on in the Agile Manifesto:  
- *Individuals and interactions* over processes and tools  
- *Working software* over comprehensive documentation  
- *Customer collaboration* over contract negotiation  
- *Responding to change* over following a plan  


###[Gitflow Branching Model](gitflow.md)  

The Gitflow branching model supports many aspects of Software Configuration Management including Source Code Management, Change control, Release engineering and Deployment.  

###[Semantic Versioning](semantic-versioning.md)  

Semantic Versioning supports Change control, Release engineering (specifically the Identifiability aspect), and Deployment among other facets of Software Configuration Management.  

###Use of GitFlow and Semantic Versioning in Continuous Integration  

**Professor Anderson**  
Due to the length of this presentation, I'm thinking of expanding it slightly using this topic, and talking GitFlow and Semantic Versioning in the context of either:
...[Fastlane.tools](https://fastlane.tools) 
or
...[Jenkins](https://jenkins-ci.org)  
