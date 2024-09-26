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
As we learned before there are multiple ways to create a Custom Connector, we will use the most basic one to learn the basics 🙂

Inside your solution click on **New** and in the menu on **Automation** and then on **Custom Connector**

!["Create new Connector"](./assets/lab02_02_createnew.png)

### General Definition
In a new tab the Custom Connector edit wizard will be openend in the first step.

!["Create Connector Wizard - Naming](./assets/lab02_02_wizardname.png)

First step is given your Custom Connector a meaningful name, make sure to use a name your users will understand, this will show up in all UIs. Bonuspoints if you also add an icon below under **General Information**

Next you need to select **HTTPS** and fill in the **Host** and **Base URL**. The Nordic Summit event api can be reached under the following url:

**https://apim-dhino-fetch-test.azure-api.net/001**

!["Adding Host and Base URL"](./assets/lab02_02_hosturl.png)

## Task 3: Define Security / Authentication
Click on **Security** on the bottom or in the wizard status on top to move on to the next step. Authentication describes how the Custom Connector will authenticate with the API and the options to chose from depends on the used API.

For the Nordic Summit Event API the authentication is done via an **API Key**, so select this option 

!["Authentication Type"](./assets/lab02_02_security.png)

After selecting you will asked to enter the label, name and location of parameter.

**Label:** This will be shown to the user when creating a new connection, shows a readable meaningful name

**Name:** This is the technical defined **by the API** so you can be creative here!

**Location:** This defines where the Custom Connector will add the API Key information when making requests. 

The Nordic Summit Event API will be authenticated by an API Key in the Header of each HTTP Request called **Ocp-Apim-Subscription-Key**

!["Api Key Setup"](./assets/lab02_02_apikey.png)

All done! Very important: **You do not need to enter any API Key in this step!** Authentication info is never stored directly in a Custom Connector but only ever in Connections. They will get created later when we are actually are using our Custom Connector.

## Task 4: Create first simple definition
Click on **Definition** to get to the next step of creating a Custom Connector, the stage where we define the actual actions which are possible to execute for this Custom Connector.

In this screen you see all actions, triggers, references and policies you have added to your connector. Since we create from Blank this screen will be empty.

Let's change that by adding our very first action by clicking on **New Action**

!["Definition Overview"](./assets/lab02_02_definitionoverview.png)

Creating an action consists of three steps:
- Naming / Description
- Request definition
- Response definition

!["Create Operation"](./assets/lab02_02_createoperation.png)

### Naming / Description
As a minimun you need to enter a unique id for this action. Choose a name which is easily recognizable and not a typical "id" because later on other actions use this id to refer to it.

We want to call the Nordic Summit Event API to get a list of all available events, which we can call it with a **GET** request to this url:
**https://apim-dhino-fetch-test.azure-api.net/001/export/query/FEC542ED-32AA-4C6D-94E5-6B3841C96B59/910D07E6-F700-404E-8B5A-7263C9DCC58A/EVENTS**

The two GUIDs in the URL are referencing the environment we want to target and we will consider them static for now, they point to the Workshop database (we weren't allowed to use the PROD database 😉)

### Request
Pick an id for this operation and we will go on the the **Request** part of it. 

The wizard has a great feature called **Import from Example** where you can copy paste an existing request (for example from documentation or lab instructions on GitHub), an the wizard will extract all needed information.

!["Create Request from Example"](./assets/lab02_02_requestexample.png)

In the opened dialog fill in the URL and HTTP method from above. Since this is a simple request with no further information you are all set to go and can click **Import**

!["Create From Example Details"](./assets/lab02_02_requestexampledetails.png)

Congrats, your connector has its first action! 🥳 Let's quickly test if we did all steps correctly so far.

### Saving and Testing
In order to test a Custom Connector you always have to save it first. If it's the first time it will actually create the Custom Connector. Do this by clicking **Create Connector**. This will deploy all resources needed in the backend and can sometimes take a bit.

!["Create Connector"](./assets/lab02_02_createconnector.png)

After the Creating is done and the loading screen is gone we can skip ahead in the Wizard navigation and jump to the final stage **Test**

Because the connector is newly created there is no Connection yet so in order to test it we first need to create one by clicking on **New Connection**

!["Test Stage"](./assets/lab02_02_testconnection.png)

This will open a new tab where you have the default Create New Connection interface like for all connectors. Which fields are shown is dependent on the selected authentication method. In our case this is the API key. Recognize the name of this field? That's the label we defined in the **Security** step! Click **Create Connection** to create it.

!["Create Connection"](./assets/lab02_02_testcreateconnection.png)

You will be redirect to the test screen. If the **Connection** field is still empty, click on the **Refresh** button and your newly created connection shows up.

With that we are ready to test! On the left hand you can select the action, and since we only have one which has no parameter you can click directly on **Test**

!["Test Operation"](./assets/lab02_02_testoperation.png)

If all is set up correct and the connection has the right API Key you will see the result of that API call with a HTTP status 200.

!["Test Result"](./assets/lab02_02_testresult.png)

First call made by your Custom Connector to the Nordic Summit event API!
