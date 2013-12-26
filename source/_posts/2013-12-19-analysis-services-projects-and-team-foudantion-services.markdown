---
layout: post
title: "Analysis Services projects and Team Foudantion Services"
date: 2013-12-19 01:49:08:47 -0200
comments: true
categories: [SSAS, TFS, Agile, Business Intelligence]
published: true
---

Working primarily with software development, this is the second time I am working in a Business Intelligence project and since the first time I missed some techniques and processes that I was used to.

Things like source control/revision, automated deployment and tests aren't common in a BI project. Most of the testing is done by hand, so imagine a bunch of records, thousands to millions and all the validation using excel or another manual approach to compare tables status. Hopefully in another post I'll talk about automating tools for testing in a BI enviroment.

In my first BI project, I had used another BI solution and code control wasn't able and migration/deployment was basically copy and paste the xml content from one enviroment to another. Now working in a Analysis Service project I decided to give a try to Team Foudation Service (The TFS online version) to see if we could bring to the project some of these techniques used in software development. Team Foudantion Service can be used free of charge with a team up to 5 members and you can create as many projects you like.

</br>
####Setting up Tools

First you need an [Outlook](http://www.outlook.com) account to create a TFS workspace at [Team Foundation Service](http://www.visualstudio.com/products/visual-studio-online-overview-vs), after that you can start creating projects. 

Now you need to download and install (if you didn't have done it yet) [SQL Server Data Tools 2012](http://www.microsoft.com/en-us/download/details.aspx?id=36843) and [Team Explorer for Visual Studio 2012](http://www.microsoft.com/en-us/download/details.aspx?id=30656).

</br>
####Creating Project

After installing the tools Team Explorer Tab is avaiable inside Data Tools. Click on "New Team Project" to create a project on Team Foudation Service.
</br>
![Team Explorer Tab]({{site.url}}/assets/images_posts/analysis-services-projects-and-team-foudantion-services/VSTeamExplorerTab.PNG)

With the project created you can go to Solution Tab, right click on solution file and click "Add Project to Source Control" and then do the first Check In. 
</br>
![Team Explorer Tab]({{site.url}}/assets/images_posts/analysis-services-projects-and-team-foudantion-services/AddingSolution2SourceControl.png)

When the proccess finish you'll have your project controlled by TFS with all the goodies of a source control system.
</br>
![files with lock icon]({{site.url}}/assets/images_posts/analysis-services-projects-and-team-foudantion-services/SolutionAdded2SourceControl.png)

Navigating to the Project TFS site, clicking on the CODE tab you can see all project files just commited.
</br>
![TFS Project Code Tab]({{site.url}}/assets/images_posts/analysis-services-projects-and-team-foudantion-services/TFSCodeScreen.png)


</br>
####More on Team Foundation Service

Source Control is just one thing you can use to support team development, TFS comes with three kinds of project management methodologies templates ready to use with your new source versioned project. Work Items (Project Tasks) can be associated with source code at Check In providing trace information about which changes in source code are related to each task.