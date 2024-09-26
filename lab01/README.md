# Lab 01 - Introduction to Custom Connectors

In this lab, you will go through the following tasks:

* Creating a new browser profile
* Logging into the account you are going to use during the workshop
* Creating developer environments
* Installing Visual Studio Code
* Installing the Power Platform Tools extension
* Connecting to the Power Platform environment
* Import your first connector

## Task 1: Create a new browser profile (Microsoft Edge)

It's always good to have a separate browser profile for your work and for workshops like this. This way you can keep all of your credentials separate and not have to worry about logging out of your personal / work accounts.

1. Open Microsoft Edge
2. Click on the profile icon on the top left corner
3. Hover over "Other Microsoft Edge Browsers" / "Other profiles" and then select **Add Browser** / **Add profile**

    ![Add new browser profile](assets/add-new-browser-profile.png)

4. Click **Add**

    ![Add a profile dialog](assets/add-profile.png)

    This will then open up a new browser window on your taskbar.

5. Pin that browser window to your taskbar
6. In the new browser window, select **Start without your data**

    ![Start without your data](assets/start-without-your-data.png)

7. Then select **Confirm and start browsing**.

    ![Confirm and start browsing](assets/confirm-and-start-browsing.png)

    It may prompt you to configure your new browser theme. If this happens, just select **Next** and then **Finish**.

## Task 2: Log on to your account

With the credentials that were provided to you, let's log into the account you are going to use during the workshop.

1. Go to [make.powerautomate.com](https://make.powerautomate.com)
2. On the sign-in screen, enter the email address that was provided to you and then click **Next**

    ![Sign in screen](assets/pa-sign-in-email.png)

3. Then enter the password and click **Sign in**
    
    ![Sign in screen](assets/pa-sign-in-password.png)

4. If you're prompted to stay signed in, click **Yes**

    You should now be logged in and on the Power Apps Home Page.

    ![Power apps home page](assets/power-automate-home-page.png)

## Task 3: Create developer environment

Developer environments are very helpful when you want to try out features, they are meant to be short living environments.

For this workshop, we are going to create a developer environment through the Power Platform Admin Center.

1. Go to the [Power Platform Admin Center](https://aka.ms/ppac)
2. Exit the Welcome / Tour pop up. You can do this by clicking on the **X** in the top right corner of the pop up screen

    ![Exit the Welcome / Tour pop up](assets/exit-welcome-tour.png)

3. Click on **Environments** in the left navigation
4. Click on **New** in the top navigation

    ![Environment + New for adding environments](assets/new-environment-button.png)

5. When the right-hand side dialog pops up - enter the following information (replace XX by the number of your user):

    | Field | Value |
    | --- | --- |
    | Name | User XX |
    | Region | Europe - Default |
    | Type | Developer |
    | Purpose | Developer environment for Nordic Summit 2024 |

    ![Create new Developer Environment](assets/create-dev-env.png)

6. Click **Next**
7. The next section is asking you to add Dataverse. Finally Click on **Save**
9. Once you have created the environment, you should see it in the list of environments. Click the **Refresh** button on the top navigation if you don't see it yet.

    ![List of developer environments](assets/list-of-environments.png)

## Task 4: Install Visual Studio Code

If you already have Visual Studio Code installed, you can skip this step.

1. Go to the [website of Visual Studio Code](https://code.visualstudio.com/download) and download the version for your device.
1. Install Visual Studio Code.

## Task 5: Install the Power Platform Tools extension

The Power Platform Tools extension is a Visual Studio Code extension that allows you to interact with the Power Platform from within Visual Studio Code. It is a very important component of the ALM story for custom connectors and for this workshop.

1. Open Visual Studio code
1. In Visual Studio Code, click on the **Extensions** icon in the left navigation

    ![Screenshot showing where the extensions above](assets/extensions-icon-on-navigation-bar.png)

2. Search for **Power Platform Tools** and then click **Install** on the **Power Platform Tools** extension

    ![TODO: Screenshot of search for Power Platform Tools](assets/power-platform-tools-search-and-religion.png)

    After installing the **Power Platform Tools** extension, you will be prompted to "Select File Icon Theme". Select any of the 2 options.

    With the Power Platform Tools extension installed, you can now interact with the Power Platform from within Visual Studio Code. But before we can do that, we need to connect to a Power Platform environment.

## Task 6: Connect to the Power Platform environment
    
1. In Visual Studio Code, click on the **Power Platform** icon in the left navigation

    ![Power Platform icon in the left navigation](assets/power-platform-icon.png)

    You'll more than likely see that there is "No auth profiles found on this computer". Let's create one.

    ![Screenshot of no auth profiles found](assets/no-auth-profiles-found.png)

2. If you don't see it open already, let's open the Terminal. Select **Terminal** in the menu on the top and select **New Terminal**

3. Type the following command in the terminal and then press **Enter**:

    ```bash
    pac auth create --deviceCode
    ```

4. You will be prompted to use a web browser to authenticate. Copy (**ctrl + c**) the ```code``` that is provided in the terminal and then **Ctrl + click** on the ```link``` that is provided in the terminal. 

    ![Screenshot of the terminal with the code and link](assets/terminal-with-code-and-link.png)

    Once you click on that link, it will open a new browser tab where you will have to paste that code into the browser and then click **Next**.

    ![Enter code and click next](assets/enter-code.png)

5. Pick the account that was provided to you by the workshop trainers. If you can't see it on screen then log in.

    ![Screenshot of the account selection page](assets/account-selection.png)

6. Then type in your password and click **Sign in**

    You will then see a page asking if you're trying to sign in to Power Platform CLI - pac. 

    ![Screenshot of the Are you trying to sign in to Power Platform CLI - pac? page](assets/sign-into-pac-cli.png)

7. Click **Continue**

    You'll then see a prompt confirming that you have successfully signed in to Power Platform CLI - pac. Close the browser tab and return to your codespace.

8. Refresh the Auth Profiles section by clicking on the **Refresh** button next to "Auth Profiles"

    ![Screenshot of the Auth Profiles section with the Refresh button](assets/refresh-auth-profiles.png)

    You should now see at least one auth profile. If you have more than one, you can select the one you want to use by clicking on the **Select Auth Profile** button next to the auth profile.

    ![Select Auth Profile](assets/select-auth-profile.png)

9. With the correct Auth Profile, in the terminal type the following command and then press **Enter**:

    ```bash
    pac env list
    ```

    This gets a list of all the environments that you have access to. You should see the **User XX** (where XX is the number of your user) environment listed as one of them. This is the one we want to eventually connect to. 

    ![Screenshot of pac org list](assets/org-list.png)

10. Take note of the Environment ID of the **User XX** (where XX is the number of your user)Environment and copy it. 

    ![Copy of Dev environment ID](assets/org-list-with-env-id.png)

11. Then in the terminal, type the following command and then press **Enter**. Make sure to replace ```00000000-0000-0000-0000-000000000000``` with the environment id that you copied above

    ```bash
    pac org select --environment 00000000-0000-0000-0000-000000000000
    ```

    You should then see confirmation that you have successfully selected the **User XX** (where XX is the number of your user) environment for the current auth profile.

    ![Screenshot of pac org select confirmation](assets/org-select.png)

12. To have further confirmation that you have successfully connected to the **User XX** (where XX is the number of your user) environment, in the terminal type the following command and then press **Enter**:

    ```bash
    pac org who
    ```
    This command will return information about the environment that you are connected to. You should see the **User XX** (where XX is the number of your user) environment listed as well as other unique information about the environment including the User email you're connected as.

    ![Screenshot of pac org who confirmation information](assets/org-confirmation.png)

## Task 7: Import your first connector

In this task, you will import your first connector.

1. Go to the [Power Automate maker portal](https://make.powerautomate.com)

1. Click on the environment on the top right (**Contoso (default)**)

1. Select the **User XX** (where XX is the number of your user) environment which you created in task 3

    ![Environment selection](./assets/select-environment.png)

1. Next, click on **More** and then on **Discover all**

    ![Discover all](./assets/more-discover-all.png)

1. Scroll down a little bit and make sure to select the **Pin** icon at Custom connectors in the data section

    ![Custom Connectors](./assets/pin-custom-connectors.png)

    This will ensure you will pin custom connectors to your left navigation and you can easily find it back.

1. Now select **Custom connectors** in the left navigation. This will open the custom connectors section in the Power Automate maker portal. From here you can see all the custom connectors that live in your environment. Currently, there will not be any, because you just created this environment. 

1. Select the **New custom connector** button and **Import from Github**

    ![Import from Github step 1](./assets/import-from-github.png)

    This will open a dialog that will enable you to import a connector from the Power Platform Connectors repository on Github we showed earlier in the presentation

1. Select **Custom** as a connector type, **dev** as the branch, **HtmlToText** as the connector and, last but not least, select the **Continue** button

    ![Import from Github step 2](./assets/import-from-github2.png)

    This will import the connector from Github and make it available for you to customize it.

1. We are not allowed to have a description shorter than 30 characters, so let's change the **Description** to `Converts HTML to plain text. This is the HTML to Text connector.`

    ![Import Html to Text connector](./assets/import-htmltotext-connector.png)

1. Explore the connector to see what's in there.

1. When done exploring, make sure to select the **Create connector** button on the top right corner

    ![Create connector](./assets/create-htmltotext-connector.png)

1. Next, we want to test out the connector. For testing the connector, we have multiple options. The technical test is in the test tab. We will talk about the other options in a later section of the workshop. Click on **6. Test** to go to the testing pane.

    Here we can see a test operation section and the actual operations. But there is a **Test operation** button that is greyed out. So we can't test our operation. Why is that? It's because we don't have a connection yet. Every connector needs a connection, even when you have a connector without authentication.

1. Select **New connection** to add a new connection for this connector

    ![New Connection](./assets/test-pane.png)

    This will enable the **Test operation** button. We can now try that out for the Html that is prefilled in the html input for the operation.

1. Select **Test operation** to test out the operation

    ![Test operation](./assets/test-pane-test-operation.png)

1. After the test is done, you are able to scroll down and see the response of the request

    ![Response operation](./assets/test-pane-test-operation-response.png)

## Next lab

This is the end of lab 01, select the link below to move to the next lab.

[⏭️ Move to lab 02](../lab02/README.md)
