# Lab 02 - Building a Custom Connector from Scratch 💪

In this lab, you will go through the following tasks:

* Create a solution
* Create a connector in the solution
* Setup authentication
* Add operation with Parameters
* Add dynamic operation

## Task 1: Create a solution
Best Practice for everything in the Power Platform: Work INSIDE solutions. They are greating for organizing your customizations and some features only work here plus they over ALM capabilities.

Because of that our first step withing **make.powerautomate.com** is to navigate to **Solutions** on the left hand side and click on **New Solution**

!["Create new solution"](./assets/lab02_conblank_01_createsolution.png)

In the dialog which open give your solution a meaningful name and select either create an own publisher by clicking **New** or use the **Default Publisher** named after your enivronment.

!["Create Solution Dialog"](./assets/lab02_conblank_02_solutionwizard.png)

Sidenote: Using the Default Publisher is not considered best practice because you have no control about the technical prefix all your components will receive.

Congrats you have a solution for doing our Custom Connector development! Every journey starts with the first step 💪

## Task 2: Create a connector from blank
