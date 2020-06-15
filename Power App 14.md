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
## Lab Prerequisites

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
   <img src="images/img3.png"/><br/>
3. Click **New** and select **Automated – from Blank**.</br>
   <img src="images/img4.png"/><br/>

### Task 2: Configure the trigger
The first thing you will need to configure is the trigger, i.e. when should this flow run. A flow can be triggered:</br>
a. manually from a Power Apps app,</br>
b. manually from a flow button,</br>
c. on a fixed schedule, or</br>
d. when an event occurs, such as a new item being added to a table, a new email arriving in a user’s inbox, a new tweet being posted that meets certain conditions, etc.</br>

In this scenario, we will configure the flow to trigger when a **new item is added** to the **Device Order entity** table in the Common Data Service</br

1. Enter a name for your flow, such as – “New device approval request”</br>
   <img src="images/img5.png"/><br/>
2. In the **Choose your flow’s trigger** box, enter **Common Data Service** and select **When a record is created - Common Data Service**.</br>
   <img src="images/img6.png"/><br/>
3. Click **Create**</br>
4. Click the **Environment** drop-down and select **Current****.</br>
5. Click the **Entity Name** drop-down and select **Device Orders**. You can type “device orders” to search for it.</br>
6. Click the **Scope** drop-down and select **Organization**. Scope allows you to limit when your flow will run, for example you could choose User and it would only run for orders you create. In this case you are choosing organization because you want this flow to run for records created by anyone in your entire organization.</br>
   <img src="images/img7.png"/><br/>

### Task 3: Add action to send an approval request
1. Click **+ New step**.</br>
   <img src="images/img8.png"/><br/>
2. Search for **Approvals** and select **Start and wait for an approval**.</br>
   <img src="images/img9.png"/><br/>
This will use the modern approval service. For more information see the blog post at Flow Modern Approvals.</br>
3. In the **Approval type** dropdown select **Approve/Reject - First to Respond**.</br>
   <img src="images/img10.png"/><br/>
4. For the Title, we will add some text and one variable. This variable will contain the Device Name of the device order request. Enter **New device request for** in the **Title** text box.</br>
   <img src="images/img11.png"/><br/>
5. Select **Device Name** for the **Dynamic content**.</br>
   <img src="images/img12.png"/><br/>
**Note:** if the Dynamic content box is not visible, click the Add dynamic content button - image</br>
6. Select the **Assigned to** field, select click **Approver**. Click on the **Add dynamic content** button to show/hide the dynamic content pane.</br>
   <img src="images/img13.png"/><br/>
You might get a warning message about this field being optional. Ignore it and ignore similar warnings in future.</br>
**Note:** Recall from the earlier lab that this will be the approver’s email address.</br>
7. Click **Show Advanced Options**.</br>
   <img src="images/img14.png"/><br/>
8. Select the **Requestor** field and select **Requested By**</br>
   <img src="images/img15.png"/><br/>
9. In the **Details** field, type **A new device has been requested** and hit <Enter>.</br>
   <img src="images/img16.png"/><br/>
10. Select **Device Name** from the Dynamic content pane.</br>
   <img src="images/img17.png"/><br/>
11. Type , **$** and select **Price**. You may need to click the **"See More"** option under the dynamic content search bar in order to see the Price option.</br>
   <img src="images/img18.png"/><br/>
12. Hit Enter and type **Department Contribution: $**</br>
13. Select **Department Contribution**.</br>
   <img src="images/img19.png"/><br/>
14. Hit Enter, type **Comments:** and select **Comments**.</br>
   <img src="images/img20.png"/><br/>
15. Your **Flow** will now look like the image below.</br>
   <img src="images/img21.png"/><br/>
16. **Save** your flow</br>

**Note:** When creating your own approval flows, you may additionally include a clickable link that will be displayed in the approval email. In this scenario, for example, you could include a link to view device details in an online catalogue. You would include the **Item link** and **Item link description**.</br></br>
**Note:** You could also set the **Item link** to deep link into a Power Apps app to view more details about the request. In this scenario, you might pass an OrderID or a DeviceID as a URL parameter. Power Apps accepts URL parameters, see Flow URL Patameters for more details.</br>

## Exercise 2: Conditional Logic
In flow, you can add conditions to take different actions depending on a certain result, in this case, whether the request was approved or rejected.</br>

### Task 1: Add conditional logic to flow
1. Click **+ New step**.</br>
   <img src="images/img22.png"/><br/>
2. Search for **Condition** and select it.</br>
   <img src="images/img23.png"/><br/>
3. Click in the left edit box that says, “Choose a value” and select **Outcome** from the dynamic content pane. You may need to press the “+” icon below the edit box to hide the dynamic content pane.</br>
   <img src="images/img24.png"/><br/>
4. Select is **equal to** for condition and type **Approve** for **Value**.</br>
   <img src="images/img25.png"/><br/>

### Task 2: Add conditional logic to flow
We will now configure what actions to perform if the response is approved or not – YES branch vs. NO branch.</br>
We will add two actions:</br>
a. Update the record in the Device Order table</br>
b. Send an email to the employee who requested the device</br>
1. In the left **If yes** box, click **Add an action****</br>
   <img src="images/img26.png"/><br/>
2. Search for **Common Data Service** and select **Common Data Service – Update a record**</br>
   <img src="images/img27.png"/><br/>
3. Select **Current** for **Environment**.</br>
4. Select **Device Orders** for **Entity Name**.</br>
5. Select **Device Order** for **Record identifier**.</br>
   <img src="images/img28.png"/><br/>
This is the unique lookup ID for the record that was created.</br>
6. Click **Show advanced options**.</br>
   <img src="images/img29.png"/><br/>
7. Select **Approve** from the **Approval Status Value** drop-down.</br>
   <img src="images/img30.png"/><br/>
8. Select the **Approved Date** field and select the **Expression** tab.</br>
   <img src="images/img31.png"/><br/>
9. Type **utcNow()** and click **OK**.</br>
   <img src="images/img32.png"/><br/>
10. In the Comments field, we want to preserve the earlier comments and append on the comments from the approver. To do so, select the **Comments** field and select **Comments**.</br>
   <img src="images/img33.png"/><br/>
11. Save the flow.</br>

### Task 3: Add another action
You will now add the send email action to the If Yes branch.</br>
1. From within the yes branch, Click **Add an Action**.</br>
   <img src="images/img35.png"/><br/>
2. Search for **send email** and select **Send an email (V2) – Office 365 Outlook**.</br>
   <img src="images/img36.png"/><br/>
3. Click **Sign in**.</br>
   <img src="images/img37.png"/><br/>
4. Click **Accept**.</br>
   <img src="images/img38.png"/><br/>
5. Click on the **To** field and click **Switch to Advanced Mode**.</br>
   <img src="images/img39.png"/><br/>
6. Select **Requested By** for To. Select from under the **When a record is created** section.</br>
   <img src="images/img40.png"/><br/>
7. Type **Your device order has been approved!** for **Subject**.</br>
   <img src="images/img41.png"/><br/>
8. Click on the **Code View** button.</br>
   <img src="images/img42.png"/><br/>
9. Set the **Body** value as shown below. Select **Device Name** and **Estimated Ship Date** from underneath the **When a record is created** header.</br>
   <img src="images/img43.png"/><br/>
**Note:** If you do not have an Office 365 mailbox setup, you can use one of the other connectors to send the email, such as Outlook.com, Gmail or SendGrid.
10. Click **Save**.</br>

## Exercise 3: Test the Flow
To test the flow, you will:</br>
a. Run the Device Ordering app and submit an approval request</br>
b. Verify the request was sent to the approver</br>
c. Approve the request</br>
d. Verify that the Common Data Service record was updated, and an email was sent back to the requestor</br>

###  Task 1: Test the Flow
**Note:** When a new device record is added to the Device Order entity in CDS, it may take up to ten minutes for the flow to trigger. To ensure the flow runs immediately, select the **Test** option in the top right and select the **“I’ll perform the trigger action”** option. Then go ahead and submit a device request. The flow should run immediately.</br>
   <img src="images/img44.png"/><br/>
1. Select **I’ll Perform the Trigger Action** and click **Save & Test**.</br>
   <img src="images/img45.png"/><br/>
2. To submit a device request, go to Make Power Apps</br>
3. Select **Apps** and start the **Device Ordering App**.</br>
   <img src="images/img46.png"/><br/>
4. Select a few devices and click Compare.</br>
   <img src="images/img47.png"/><br/>
5. Select one of the devices, provide email for Approver.</br>
   <img src="images/img48.png"/><br/>
6. Provide a comment and click Submit device request.</br>
   <img src="images/img49.png"/><br/>
7. Click **OK**.</br>
8. The flow will run and send email to the manager email you provided. The request for approval email will look like the image below; it will include **Device information, Price, Department Contribution (the calculated field), and the Requester Comment**.</br>

**REMINDER:** If the flow does not run immediately, please wait, it may take up to ten minutes for the flow to be triggered. To ensure the flow runs immediately, see note above - select the **Test** option in the top right and select the “I’ll perform the trigger action” option. Then go ahead and submit a device request. The flow should run immediately. The email, however, may take a few minutes to appear regardless of when the flow starts.</br>
   <img src="images/img50.png"/><br/>
9. Click **Approve**.</br>
10. Add a comment and click **Submit**.</br>
   <img src="images/img51.png"/><br/>
11. The flow will continue to run; it will update the record and send an email to the requestor. The email sent to the requester will look like the image below.</br>
   <img src="images/img52.png"/><br/>
12. Check the flow, you will notice that the flow is now marked as **Succeeded** in the run history.</br>
   <img src="images/img53.png"/><br/>

## Exercise 4: Update the Flow
In this exercise, you will add two actions to the “if no” branch.</br>

### Task 1: Add actions
1. If you don’t already have the flow open, open it in edit mode.</br>
   <img src="images/img54.png"/><br/>
2. In the If no branch, click **Add an action****.</br>
   <img src="images/img55.png"/><br/>
3. Search for **Common Data Service** and select **Common Data Service – Update a record**.</br>
   <img src="images/img72.png"/><br/>
4. Select **Current** for **environment, Device Orders** for **Entity Name**, select **Device Order** for **Record Identifier**, and click **Show advanced options**</br>
   <img src="images/img57.png"/><br/>
5. Select **Reject** for **Approval Status Value**.</br>
   <img src="images/img58.png"/><br/>
6. Click **Add an action**.</br>   
<img src="images/img59.png"/><br/>
7. Search for **send email** and select **Send an email (v2) - Office 365 Outlook**.</br>
   <img src="images/img60.png"/><br/>
8. Provide the information shown on the image below. This will send an email to the requestor informing them that their device request was not approved. Select Requested By and Device Name from under the **When a record is created** header.</br>
   <img src="images/img61.png"/><br/>
9. **Save** the flow.</br>

### Task 2: Test the updated Flow
1. Click **Test** in the top right of the flow editor and start the Flow.</br>
2. Run the Device Ordering app -> Select a device and submit an approval request.</br>
3. You should receive an email with options to Approve or **Reject** the request. Select Reject this time and enter some comments, such as “Not eligible for new device.” Click Submit.</br>
   <img src="images/img62.png"/><br/>
4. Confirm that the requestor receives an email informing them that their device approval request was rejected.</br>
   <img src="images/img63.png"/><br/>
5. Navigate to Make Power Apps select **Apps** and start the **Device Procurement** application.</br>
   <img src="images/img64.png"/><br/>
6. Device Orders will now have the Approval Status.</br>
<img src="images/img65.png"/><br/>

### Task 3: Visit the approval center
1. Use the Device Ordering app to **submit a few more approval requests**.</br>
2. Navigate to Power Automate and make sure you are in the correct environment. Login with your lab credentials if prompted.</br>
3. Expand **Action items** and select **Approvals**.</br>
<img src="images/img66.png"/><br/>
4. Notice that all pending approval requests are visible.</br>
<img src="images/img67.png"/><br/>
5. Go ahead and approve or reject a request from this screen. The details are displayed in the right pane where you] can **enter comments** and **Confirm**.</br>
<img src="images/img68.png"/><br/>
6. The request will no longer be visible as it has been processed.</br>
**Note:** All approval requests sent to the current logged on user will be visible in the Approvals Center. This includes approvalssent from any app or flow.</br>
7. You can also use the Approvals Center to view all requests that you have sent and are **Awaiting response** from the approver. Select the **Sent requests** tab at the top to view all requests that you have sent.</br>
8. Open the **Power Automate mobile app** on your mobile device.</br>
9. Login and switch to the environment where the flow is deployed.</br>
<img src="images/img69.png"/><br/>
10. Select **Approvals** in the top right and view all pending approvals.</br>
<img src="images/img70.png"/><br/>
11. You can quickly approve or reject these pending requests from this screen.</br>
<img src="images/img71.png"/><br/>
12. If you have push notifications turned on and are signed into the flow mobile app – when you receive a new Approval request it will trigger a push notification on your phone. You can give this a shot.</br></br>
Congratulations! You have successfully completed this lab. You have created your Power Apps app and flow and connected them to a Common Data Service entity. Now you are ready to build your own apps and workflows.</br></br>

## Lab survey
We would appreciate your feedback on the Business Application Platform technologies and on this hands-on-lab, such asthe quality of documentation and the usefulness of the learning experience.</br>

Please use the survey at App in a day survey to share your feedback.</br>

You may provide feedback for each module as you complete it or at the end once you’ve completed all the modules.Thank you!</br>

**References**
App in a Day introduces some of the key functionalities available in Power Apps, Power Automate, Power BI and theCommon Data Service. For an up to date list of learning references, see Power Apps Resources and Power Automate</br>

## Copyright
By using this demo/lab, you agree to the following terms:
The technology/functionality described in this demo/lab is provided by Microsoft Corporation for purposes of obtaining your feedback and to provide you with a learning experience. You may only use the demo/lab to evaluate such technology features and functionality and provide feedback to Microsoft. You may not use it for any other purpose. You may not modify, copy, distribute, transmit, display, perform, reproduce, publish, license, create derivative works from, transfer, or
sell this demo/lab or any portion thereof.</br>

COPYING OR REPRODUCTION OF THE DEMO/LAB (OR ANY PORTION OF IT) TO ANY OTHER SERVER OR
LOCATION FOR FURTHER REPRODUCTION OR REDISTRIBUTION IS EXPRESSLY PROHIBITED.
THIS DEMO/LAB PROVIDES CERTAIN SOFTWARE TECHNOLOGY/PRODUCT FEATURES AND FUNCTIONALITY,
INCLUDING POTENTIAL NEW FEATURES AND CONCEPTS, IN A SIMULATED ENVIRONMENT WITHOUT
COMPLEX SET-UP OR INSTALLATION FOR THE PURPOSE DESCRIBED ABOVE. THE TECHNOLOGY/CONCEPTS
REPRESENTED IN THIS DEMO/LAB MAY NOT REPRESENT FULL FEATURE FUNCTIONALITY AND MAY NOT
WORK THE WAY A FINAL VERSION MAY WORK. WE ALSO MAY NOT RELEASE A FINAL VERSION OF SUCH
FEATURES OR CONCEPTS. YOUR EXPERIENCE WITH USING SUCH FEATURES AND FUNCTIONALITY IN A
PHYSICAL ENVIRONMENT MAY ALSO BE DIFFERENT.</br>

**FEEDBACK.** If you give feedback about the technology features, functionality and/or concepts described in this demo/lab to Microsoft, you give to Microsoft, without charge, the right to use, share and commercialize your feedback in any way and for any purpose. You also give to third parties, without charge, any patent rights needed for their products, technologies and services to use or interface with any specific parts of a Microsoft software or service that includes the
feedback. You will not give feedback that is subject to a license that requires Microsoft to license its software or documentation to third parties because we include your feedback in them. These rights survive this agreement.</br>

MICROSOFT CORPORATION HEREBY DISCLAIMS ALL WARRANTIES AND CONDITIONS WITH REGARD TO THE
DEMO/LAB, INCLUDING ALL WARRANTIES AND CONDITIONS OF MERCHANTABILITY, WHETHER EXPRESS,
IMPLIED OR STATUTORY, FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT.
MICROSOFT DOES NOT MAKE ANY ASSURANCES OR REPRESENTATIONS WITH REGARD TO THE ACCURACY
OF THE RESULTS, OUTPUT THAT DERIVES FROM USE OF DEMO/ LAB, OR SUITABILITY OF THE INFORMATION
CONTAINED IN THE DEMO/LAB FOR ANY PURPOSE.</br>

#### DISCLAIMER
This demo/lab contains only a portion of new features and enhancements in Microsoft Power Apps. Some of the features might change in future releases of the product. In this demo/lab, you will learn about some, but not all, new features.
