# Lab 03 - Testing and Troubleshooting a Custom Connector 🚨

In this lab, you will go through the following tasks:

* Add dynamic operation
* Using the test pane in the custom connector UI
* Testing a Custom Connector in Power Automate
* Testing a Custom Connector in Power Apps
* Increase the Custom Connector usability

## Task 1: Making an action dynamic
In Lab 2 we added an action with a parameter but noticed the usability was subpar. One way to improve is to replace the manual input field with **Dynamic Values** which are a drop-drown which is not hardcoded but instead uses value from another action.

Basically, we want to achieve this when someone uses this action:
- Make a call to the **Tracks** action to get available Tracks
- Instead of their Id display a readable Description or Name
- When making the call to the SessionByTrack API send the id instead of the displayed Name.

Let's built this! 🙂

We start back on the **Definition** page, select the SessionByTrack action and open the parameter:

!["Edit Parameter"](./assets/lab03_01_editparameter.png)

On the detail page we will take a more detailled look at the dropdown types. With these we can change the field from manual input to a dropdown from which a user can easily select a value.

!["Dropdown Types"](./assets/lab03_01_dropdowntypes.png)

The following options are available

- **Disabled**  Default value, no dropdown, just manual input
- **Static** Dropdown, values must hardcoded in the custom connector. No way to differentiate between id and displayname
!["Static Dropdown"](./assets/lab03_01_staticdropdown.png)
- **Dynamic** Dropdown, but this time the values are provided during runtime by another action 👍

We will use the **Dynamic** option in this case.
- Select our GET/Tracks action as **Operation Id** (that's why operation id names are important!)
- The **Value** can be picked from the field we defined as the default response in the GET/Tracks action. If there is no response defined, this feature can not be used! In this case we use the **id** property of the Track because the API is requiring this value.
- The **Value Display Name** will be the field which is only used for the user to make it easier to pick the right value. In our case we use the **Name** property of the Track

!["Dynamic Dropdown"](./assets/lab03_01_dynamicdropdown.png)

Awesome let's **Update Connector** and go to our Test page!

## Task 2: Test using the Test page within a Custom Connector

Sadly, these (and most of the other UI features) are not supported here 🙁 The Test pages is only for Developers and supports only manual inputs.

!["Test Console Dynamic"](./assets/lab03_01_testconsole.png)

🏆 for the shortest task in this workshop, but let's look at the other option we can use for this 👍

## Task 3: Testing in Power Automate
Power Automate, more specifically Power Automate Cloud Flows is probably the tool using Custom Connectors the most. In order to create our test flow, navigate to your solution (remember the best practice: Everything inside solutions!), by selecting **Solutions** on the left hand side and opening your created solution from Lab 02.

!["Navigate to Solution"](./assets/Lab03_02_solution.png)

In your solution you should already see your connector 🙂 (sometimes the UI takes a bit to refresh)

!["Custom Connector in Solution"](./assets/lab03_02_customconnector.png)

We are going to add a new **Manuel Flow** by clicking on **New** -> **Automation** -> ** Cloud Flow** -> **Manual**

Manual means that the flow can be trigger manually via the UI which is usually the easiest for testing and debugging.

!["Add Flow"](./assets/lab03_02_addflow.png)

In the creation wizard give the Flow a meaningful name and make sure the trigger **Manually trigger a flow**

!["Name Flow"](./assets/lab03_02_flowname.png) 

### Building the Flow

Within our Flow editor we want to add a **New Step**

!["New Step"](./assets/lab03_02_newstep.png)

Here you find all available connectors. On the tab **Custom** is our newly created Custom Connector. Here is also a great example why images for custom connectors are important, it helps **a lot** with the discoverability, especially if you have many!

!["Custom Connector Selection"](./assets/lab03_02_selectcustom.png)

After selecting our Custom Connector we see all available actions we did define in it. Select our GET/SessionsByTrack action.

!["Available actions"](./assets/lab03_02_actions.png)

The first time you use a Custom Connector in Power Automate you must create a new connection for security reasons. You can choose any name and reuse the API Key from before.

!["Action Connection"](./assets/lab03_02_connection.png)

After we created the connection we do see our parameter field, but this time it is displayed as a dropdown!

!["Dynamic Values"](./assets/lab03_02_dynamicsvalues.png)

Notice that the values are displayed by their name and not the id even if the API is requiring the id. Let's **Save** our Flow and then do a **Test**.

!["Save flow and run test"](./assets/lab03_02_saveandtest.png)

In the Test dialog select **Manually** and then **Run Flow**. If you work with input or automatic trigger the **Automatically** option is powerful because you can easily restart the flow with previous inputs. But for now we are going with Manually.

!["Flow Test Run Dialog"](./assets/lab03_02_runtest.png)

After confirming that you want to run the flow you can close the dialog and will see the results within the editor. You can click on single actions to inspect their in- and outputs.

!["Flow Success"](./assets/lab03_02_flowsuccess.png)

Because we defined the Reponses of all our our actions it's also pretty easy to combine them. For example we can use the GET/Tracks action to get an array of all tracks and then iterate through them to get all sessions per track.

For this we add the GET/Tracks action above our GET/SessionsByTrack action and want to use it's output in it. For this you have to select **Enter Custom Value** in the dynamics dropdown to dynamically fill this value (🤪)

!["Custom Value"](./assets/lab03_02_customvalue.png)

And because we defined the response properties of our GET/Tracks action we can now select them nicely in the UI.

!["Dynamic Values"](./assets/lab03_02_customdynamic.png)

And the Custom Connector also knows that GET/Tracks returns an array, so it automatically wraps the action in an **Apply to Each**

!["Apply To Each"](./assets/lab03_02_applytoeach.png)

## Sidequest: Increase the UX with user-friendly names
One thing you could quickly tell was that our clear **operation ids** are not very user friendly in these kinds of UIs. But the great thing is that we can actually do something about this and within the Custom Connector add more information. For this we will go back to our Custom Connector, edit it, and go to definitions to update our Actions.

First we will create more detailled descriptions of the actions themselves. With these you can give your action friendly names and also provide additional explanations which will be displayed as extended texts or tooltips. And of course these descriptions are immensly important for any AI you want to use your Custom Connector with.

!["Action Details"](./assets/lab03_03_actiondetails.png)

You can do the same with parameters or response properties if you go into the edit mode of those. You can also control the **Visibility** to either hide or promote actions.

!["Visibility"](./assets/lab03_03_visibility.png)

Visibility in Power Automate will be displayed like this

!["Visibility in Power Automate"](./assets/lab03_03_visibilitydisplay.png)

So by taking care of these properties, you make your connectors a lot easier to use and more professionally looking. But at the same time, you also prepare them for AI 🙂




