---
layout: post
title: "Integrating Oracle Data Integrator and Analysis Services"
date: 2015-02-01 17:05:17 -0200
comments: true
categories: [Business Intelligence, ODI, Automation, Analysis Services, SSAS]
published: true
---


In this post I'd like to show a simple integration between [Oracle Data Integrator](http://www.oracle.com/technetwork/middleware/data-integrator/overview/index.html) and [SQL Server Analysis Services](http://www.microsoft.com/en-us/server-cloud/solutions/business-intelligence/analysis.aspx) that enables a SSAS cube or dimension to be processed from inside ODI packages.<!-- more -->

</br>
####Motivation

In medium and large environments, companies tend to use tools from one vendor only. This approach have its benefits as built-in integration - mostly of the time - between tools and a single point of support. Moreover, find skilled workers that can handle with tools from same vendor stack is easier. 

Although the scenario described above is probably the best case, sometimes companies choose to use solutions from others vendors to deal with specific issues. Therefore, in these situations some questions like lack of integration and tools that overlap some of its features may arise.

</br>
####The Solution

Though some configurations in ODI and SSAS must be done in order to get the integration, it basically consists in a ODI procedure coded in Jython that does a http request to SSAS passing a xmla script.

First we need to enable SSAS to accept xmla request over http. I won't show how to to this, but you can get more information [at MSDN](http://msdn.microsoft.com/en-us/library/gg492140.aspx) or just google ["configure http access to analysis services"](http://www.google.com.br/webhp?#q=configure+http+access+to+analysis+services). 

Note that when configuring authentication type for the IIS application, it must be set to anonymous and a user account should be used to impersonate the connection. This account will be used later to set up processing-cubes permissions in SSAS databases.

For security reasons, the account used to configure IIS application must have only process permissions, so we need to create a role in SSAS database and allow it to process all cubes and dimensions. Leave the ```Access``` and ```Local Cube / Drillthrough``` both set to ```None``` and check ```Process``` for all cubes in database. After that, just add the user account used earlier as a member of this role.
![Creating SSAS Role]({{site.url}}/assets/images_posts/integrating-oracle-data-integrator-and-analysis-services/creating-ssas-role.png)

If you plan to use more the one environment you will need to configure one web application for each of them.

Second step is to configure ODI. This is not mandatory, but if you have more than one environment, like QA and Production, it will help you coping deployment questions when migrating from one environment to another.

The ODI configuration lies just in creating a flexfield for contexts where we should place the url where the SSAS responds to http requests. Therefore, in an ODI QA environment you can set the url to call a SSAS instance used only for test or QA purpouses. When the package is deployed at production level, the flexfield context in this environment should be configured with the url pointing to the production instance of SSAS.

![Creating Flexfield in ODI Context]({{site.url}}/assets/images_posts/integrating-oracle-data-integrator-and-analysis-services/configuring-flexfield-in-odi-context.png)

After create the flexfield you can configure it with the SSAS url:
![Configuring SSAS URL in ODI Context]({{site.url}}/assets/images_posts/integrating-oracle-data-integrator-and-analysis-services/configuring-ssas-url-in-context.png)

The procedure code is simple. It just wraps a xmla script and completes it with the database and cube names and the processing option.
{% gist 7a310c8794ad7306f119 %}

Now just drop the procedure into a ODI scenario and configure the Options with your own information:
![Configuring SSAS URL in ODI Context]({{site.url}}/assets/images_posts/integrating-oracle-data-integrator-and-analysis-services/using-procedure.png)

That's it! Now you can use ODI to process SSAS objects. Below you can download the procedures to process both Cubes and Dimensions.
[Download ODI Procedures]({{site.url}}/assets/images_posts/integrating-oracle-data-integrator-and-analysis-services/ODI Procedures.zip)

I would like to thanks my colleague [Guthierry Marques](https://github.com/GuthierryMarques) who helped us develop these procedures. Thanks buddy!