# Module 4: Power Automate

## Contents
**Power Automate**</br>
Lab Prerequisites</br>
Exercise 1: Create Approval Request Flow</br>
Exercise 2: Conditional Logic</br>
Exercise 3: Test the Flow</br>
Exercise 4: Update the Flow</br>
**Lab survey**</br>
**References**</br>
**Copyright**</br>

# Power Automate
## Lab Prerequisites</br>

This is the fourth lab in a five-part series covering Power Apps, Common Data Service, and Power Automate. The assumption is that you have successfully completed the first three modules, or at least the initial part of setting up an environment as described in the overview – **“00-AppInADay Lab Overview.pdf”**.</br></br>
If you have not completed the previous modules, you can use the partially completed version of the lab package in the“\Completed\Module3” folder. Follow the instructions in the document “Importing Module 3 Completed” before proceeding with this module, which will provision the app and the Common Data Service entity into your environment.</br></br>

## Integrating a Power Apps App with Power Automate
In this lab, you will create a flow that uses the Modern Approvals service to automate the approval workflow – it will send an email to the selected approver and take an action based on their response.</br>
You should already have an app with these two screens:</br>
   <img src="images/img1.png"/><br/>

## Exercise 1: Create Approval Request Flow
The flow will trigger when a new item is added to the **Device Order** entity table in the Common Data Service.</br>
• It will use the Approvals Service to send an approval request.</br>
• The approver will receive an email with options to Approve or Rejects and add comments.</br>
• Once the approver responds, the record in the Device Order table will be updated with the appropriate approval status and comments.</br>
• An email will be sent to the requester informing them whether the device was approved or rejected.
There are two ways to create a flow – from blank or from a template. In this lab, we will create the approval flow starting with a blank flow.</br>

### Task 1: Login on Power Apps website and create a flow
1. Navigate to Make Power Apps and make sure you are in the correct environment.</br>
   <img src="images/img2.png"/><br/>
2. Select **Flows**.</br>
3. Click **New** and select **Automated – from Blank**.</br>

### Task 2: Configure the trigger
The first thing you will need to configure is the trigger, i.e. when should this flow run. A flow can be triggered:</br>
a. manually from a Power Apps app,</br>
b. manually from a flow button,</br>
c. on a fixed schedule, or</br>
d. when an event occurs, such as a new item being added to a table, a new email arriving in a user’s inbox, a new tweet being posted that meets certain conditions, etc.</br>

