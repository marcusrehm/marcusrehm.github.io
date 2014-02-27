---
layout: post
title: "ODI+ DbFit = ELT + Automated Tests"
date: 2013-12-23 16:44:48 -0200
comments: true
categories: [Agile, TDD, Business Intelligence, ODI, DbFit]
published: false
---


####ETL Testing
ETL testing can be a painfull job when you have to test packages that manipulate hundreds or thousands of records and most of the time it is a manual job.

The common test scenario that I know (and I see a lot of people doing) is to run a query on source data base, do the same with the target data base put the results in a Excel worksheet and then compare them. For a few rows it's fast and easy, but when we are talking about hundred or more rows it becomes a nightmare.

Even if you have a macro or script to compare this data sets the manual steps to run these queries and put the rows into a worksheet need to be done manually and even if it can be automated in a worksheet you will end up with a large number of worksheets, macros, scripts and so on.

Another drawback in this approach is that these Excel worksheets or scripts used by each developer or tester to compare source and target data are created and used only by their owners and may not follow a pattern leading to issues to exchange this artefacts between team members.

In this scenario even small changes in ETL process demands a whole new round of tests execution.
</br>
{% img center http://4.bp.blogspot.com/_ck61awodl-U/THQjSTqwaZI/AAAAAAAAACA/7md6qttC9lg/s320/charlie-brown.jpg %}

Now imagine if we have a tool (and we have) that enable us to create tests like the scenario described above but in a way we can write once and execute as many times we need just clicking a button. Even more, imagine if with this tool we can have a centralized repository to share these tests with other team members so they can use it in the future to validate the ETL process after a change made in code.

</br>
####Fitnesse/DbFit
[FitNesse](http://fitnesse.org/FrontPage) is a open source [Acceptance Testing Framework](http://en.wikipedia.org/wiki/Acceptance_testing) built up in a wiki style where each wiki page can be of type statical, test or suite. Basically Statical pages can have only text information and test pages can have both text information and executable code. The suite page type is just an aggregation of test pages that can be run as a package.

Being a wiki, FitNesse is very easy to be used by both developers and business users so it can act as a centralized repository for specifications and tests. As the FitNesse site itself says *"The wiki pages created in FitNesse are run as tests. The specifications can be tested against the application itself, resulting in a roundtrip between specifications and implementation"*.

[DbFit](http://dbfit.github.io/dbfit/index.html) is a set of FitNesse fixtures that enables developers to create unit and integration tests for database objects. This way, queries, procedures and CRUD statements can be specified and tested in a test-driven approach.

For our ETL scenario, DbFit fixtures are what we care about.

</br>
#####A Pratical Example
Let's say we are developing a ETL job to load 

</br>
####Executable Specifications

</br>
####Running in Production Enviroment
In this [post](http://blog.quickpeople.co.uk/2013/12/06/dbfit-for-prod-tests/) Jake Benilov, the main maintener of DbFit, talks about pros and cons about use DbFit in production enviroments.