---
layout: single
title:  "How to manage software quality"
date:   2018-02-18 8:00:00 +0100
categories: management
header:
    overlay_image: /assets/images/code-quality.jpeg
    show_overlay_excerpt: false
    overlay_filter: rgba(0, 0, 0, 0.5)
    teaser: /assets/images/code-quality-teaser.jpeg
---

At the heart of the software project lifecycle is the development phase. I have described how to get to this phase in my previous post on [How to start new projects](/management/2018/02/13/starting-new-projects.html). In this article I'm going to dive deeper into the development phase with focus on how to prevent project failures due to insufficient software quality. 

As with many things in the industry, it starts with the right mindset. So what is this software quality mindset?

## Software quality mindset

There is a common mistake made by some software developers and managers. They often forget to include software quality as a part of the development process. 

Many developers tend to believe that their code is so perfect that they do not need any quality checks. They estimate the time needed to write the feature and do not include any time for writing or updating tests. Later the code fails horribly in production due to trivial and totally avoidable errors. **Believing in quality is not enough. It has to be measured.** There are many tools for measuring the code quality and a professional developer has to use them and to prevent code issues in the future.

This is also typical for the project managers, IT leads and CTO's. They often overlook the fact that their projects have no quality measurements and do not enforce them. They might blindly trust their developers (or external vendors) to do the right thing and never even ask about it. Asking the developers about software quality could be uncomfortable, but it is necessary. **The manager should be able to validate the quality of the product that he is responsible for.**

Having the software quality mindset means that both developers and managers actively measure and prevent any technical issues with the software. Having a dedicated [Quality assurance](https://en.wikipedia.org/wiki/Quality_assurance) person on the team is good, but quality should be measured on all levels. Software projects  should try to avoid the creation and accumulation of **technical debt**.


## Technical debt

Technical debt is the potential cost of having to do any additional rework. Lack of quality measurements is one of the causes for its accumulation. It is very hard to eliminate it in later stages of the development and it might become a major reason for a complete rewrite or even cancellation of the project as dealing with the debt becomes too expensive. Managing technical debt is at the core of high quality software development. Developers can help reduce the technical debt by actively maintaining a suite of **unit tests**.


## Unit tests

Unit tests are small scale procedures (in code) written by the developer to verify the functionality and capture any potential mistakes. They are focused on the smallest testable part of an application. The unit could be an individual function, module or a particular feature. These tests should be the primary quality checks for the developer. They enable to **test the correct "happy path"** and **also other "problematic paths"** to see how the code behaves in these scenarios.
A well maintained test suite also helps new developers to quickly understand what each part of the code is doing.

_There are too many ways a part of the code could break. Having an automated test that covers most of the possible scenarios is very beneficial._

Important tool in unit testing is [Mocking](https://en.wikipedia.org/wiki/Mock_object). In general it means replacing components of the application with a mimic version for running tests. For example replacing a real database connection with a fake connection which acts as a real database. If the component cannot be properly mocked it could be an indicator that our code is not modular enough and this might become a problem in the future ([Code Smell](https://en.wikipedia.org/wiki/Code_smell)).

The other big benefit is that executing a suite of unit tests is much faster than building and deploying the entire application.
This enables the developer to do small changes and test them rapidly.

[Test-driven development](https://en.wikipedia.org/wiki/Test-driven_development) is one of the popular approaches the developers could choose. In TDD the tests are written before the actual code. The adoption of the methodology really depends on the team. In the end what is important is the the software has a reasonable amount of **code coverage**.


## Code coverage

Code coverage is measured as a percentage of tested vs. untested code. Various tools can measure this automatically and even highlight the parts of the code which are not covered. There are many ways to configure the code coverage for different languages and editors. For example, for [PyCharm](https://www.jetbrains.com/pycharm/) there is a section in the [documentation](https://www.jetbrains.com/help/pycharm/configuring-code-coverage-measurement.html).

For different editors there are other settings, plugins or standalone tools that enable code coverage measuring.

Also a standalone **continuous code quality tool** like [SonarQube](https://www.sonarqube.org/) provides code coverage as one of its features.


## Continuous code quality tools

Having automated code quality measurement executed as part of the build process is invaluable. Running automated checks after each code commit is a good way to notify developers of potential problems. Also having a dashboard with detailed quality measurements gives the project manager good visibility of the current code quality and how it is changing over time.

One of the most recommended code quality tools is [SonarQube](https://www.sonarqube.org/) which has a lot of useful features for detecting various code problems, bugs and vulnerabilities. This feature is called **static code analysis**. The tool checks the code without actually executing it. 

While unit tests and static code analysis cover most of the **code quality**, it is important to measure the overall **software quality** as well. It is necessary to verify that the business logic is correct, the UI works correctly and the overall performance is acceptable.
This is done using **integration tests**, **UI tests** and **performance tests**.


## Integration testing

Integration testing means assembly of all the application components and testing the solution as a whole. These tests are more complex and usually are executed on dedicated testing environments. These environments should resemble the actual production environment as closely as possible to avoid any unwanted regression. 

Part of integration testing is creating a detailed **test plan**. The steps in the test plan are closely related to the real world use-cases of the application.


## User interface testing

In the past it was pretty common to test the user interfaces of applications manually. The test plan was a document of steps that the human tester had to follow. Complex business applications required a lot of human testers to follow the test plans and note any possible errors. Nowadays we have **automated tools** that are much faster and much less error prone than human testers. The most popular tools for testing the user interfaces are:
- [Selenium](http://www.seleniumhq.org/)
- [Robot Framework](http://robotframework.org/)
- [Tricentis Tosca](https://www.tricentis.com/)


## Performance testing

Part of software quality measurements is also performance testing. Performance tests are designed to measure the stability and responsiveness of the application under a particular workload. Using these tests it is possible to investigate the scalability and reliability of the software. The results may have a major effect on the future evolution of the software and could lead to major changes in the architecture of the application. 

Most importantly, performance tests can uncover many potential issues which could not have been detected by small scale unit or UI tests.

Some common tools for automated performance testing are:
- [Apache JMeter](http://jmeter.apache.org/)
- [Gatling](https://gatling.io/)

## Summary

In this article I have described various ways to manage software quality during the development phase.
I will summarize them in the following points:
- Software quality mindset means careful measurement of the quality using specialized tools
- Developers should write unit tests and monitor the code coverage
- Static code analysis tools help with discovering common bugs, code smells and vulnerabilities
- Integration testing is testing of the complete solution in a real environment
- UI testing is important to verify the user interface and should be automated
- Performance testing can uncover potential stability and scalability issues

My final advice is **automate as much of this as possible**. Running these tests could be a part of a complete [Continuous integration](https://en.wikipedia.org/wiki/Continuous_integration) cycle. I will talk about this in another article. I hope that this article gave you some valuable information on how to measure the software quality and I wish you good luck on your projects!
