## Exercise 2 - Learn Publish-Subscribe pattern using S/4 HANA, AEM and Cloud Integration
In this exercise, we will learn an end-to-end publish-subscribe pattern using S/4 HANA, AEM and Cloud Integration. We will publish a Business Partner Change event from S/4Hana to an AEM topic using RAP-based events. The event will then be sent from the topic to two queues, which act as topic subscribers. Finally, two independent subscribers will receive the event by listening to their respective queues.

## Exercise 2.1 - Create new Queue in Advanced Event Mesh for second subscriber
After completing these steps you will have created a queue in Advanced Event Mesh.

1. Go back to the original tab in your browser of AEM and click on **"Cluster Manager"** on the left.
2. In the All Services screen click on the **"Broker Asia"** tile.

	**HINT:** If you cannot see the tiles, uncheck the "**Only show my services**" box.

	![](./images/ex3-1.png)

3. Switch to **"Manage"** tab and click on the **"Queues"** button. A new browser tab/window will open.

   ![](./images/ex3-2.png)

4. Click the **"+ Queue"** button on the top right.

   ![](./images/ex3-3-2.png)
   
5. In the pop up enter the queue name: **User_XXX_WebApp** (replace **XXX** with your assigned user number) and click **"Create"**

   ![](./images/ex3-3-3.png) 

6. On the next screen keep all the default settings and click **"Apply"**

	![](./images/ex3-3-1.png)       

7. Find the queue in the list that you crated in the previous step and click on it. 

   ![](./images/ex3-3-4.png)  
   
8. Switch to the **"Subscriptions"** tab and click on **"+ Subscription"**.

   ![](./images/ex3-3-5.png)  

9. Enter following topic: **"s4/t41/400/ce/groupXX/BusinessPartner/Changed/v1"** (replace **XX** with your assigned user number). Click on **"Create"**.

	![](./images/ex3-3-6.png)

10. Simlarily subscribe to the same topic **"s4/t41/400/ce/groupXX/BusinessPartner/Changed/v1"** in the first queue **"User_XXX"** (replace **XXX** with your assigned user number) that you created in Exercise 1.2

	![](./images/ex3-3-7.png)

## Exercise 2.2 - Configure Publishing of S/4 HANA Business Partner Change event to AEM using RAP based events

1. Log into **WTS**

   Link: https://class.learning.sap.com/my.policy
   <br>System : **SY-S42023FPS2BGACC-WS001**
   <br>Username : **WS-XXX** where **XXX** is your assigned user number
   <br>Password: provided by the moderator
   
   **Note:** In case you get the error that **"Your session could not be established."**, open a new session

   ![](assets/20250818_233959_image.png)
   <br><br>![](assets/20250818_234051_image.png)

3. After successfull login

   ![](assets/20250818_235320_image.png)
   
4. Search for **SAP HANA Studio** and open the version **2.3.78**.

   ![](assets/20250818_235357_image.png)

5. Verify if workspace name is **“AEMXX”** where **XX** is your assigned user number. Click on Launch.
   **Note:** In the screenshots, we are using 01 group as example.

   ![](assets/20250818_235456_image.png)

   If the below pop-up appears, select **“Ask me later”**

   ![](assets/20250818_235538_image.png)

6. To open the imported project, double click on the project on left side and enter the password: **Welcome1** and click on “OK”.

   ![](assets/20250818_235606_image.png)

7. Expand **“Favorite Packages”**.

   ![](assets/20250818_235639_image.png)

8. The package of RAP Objects imported (**Z_RAP_AEM_WORKSHOP**) can be seen. Expand it.

   ![](assets/20250818_235700_image.png)

9. Expand **“Business Services”**.

   ![](assets/20250818_235721_image.png)

10. Expand **“Event Bindings”**.
    <br>**Note:** You can close the last two tabs for better view.

    ![](assets/20250818_235746_image.png)

11. Double click on the event binding **Z_AEM_BP_CHANGED_GROUPXX** (where **XX** is your group number).
    <br>**Example is for Group/User 01** :

    ![](assets/20250819_001130_image.png)

12. Click on **Save** and **Activate** the object.
    <br>Use the activation button ![](assets/20250819_001428_image.png) from the tool bar

## Exercise 2.3 - Configure First Subscriber using Cloud Integration capability of SAP Integration Suite
In this exercise, an Integration Flow is added as a subscriber via the Advanced Event Mesh adapter using the Solace Messaging Format (SMF). Integration flows can be used to mediate events, for example, to perform message transformation or protocol conversion steps.

### Exercise 2.3.1 - Setup REST Endpoint

Before we start building our integration flow, we will "provision" a simple HTTP endpoint where we will send the message.

1. **Webhook.site (HTTP endpoint)**

    For simplicity purposes, our REST consumer will be a simple HTTP endpoint that will receive the messages from the queue. We will use a tool called [Webhook.site](https://webhook.site/) to create a temporary endpoint that will receive the messages. When you navigate to the website, you will be presented with a unique URL that you can use to receive the messages. **Take note of the unique URL** as we will use it to configure the REST consumer.
    
    <p align = "center">
        <img alt="webhook.site example" src="images/webhook-site-example.png" width="100%"/><br/>
        <i>webhook.site example</i>
    </p>

### Exercise 2.3.2 - Create Integration Package in Cloud Integration capability of SAP Integration Suite

1. Open the SAP Integration Suite landing page via this [link](https://cpisuite-europe-03.integrationsuite.cfapps.eu20-001.hana.ondemand.com/shell/home).

   ![](./images/ex2-1.png)

2. Navigate to **Design > Integrations and APIs**, and select **Create**.

   ![](./images/ex2-2.png)
   
3. Fill the following:
   <br>**Name:** "User**XXX**" where **XXX** is your assigned user number
   <br>**Short Description:** "Integration Package for event mediation from User **XXX**".

   <br>click **Save**.

   ![](./images/ex2-3.png)

### Exercise 2.3.3 - Copy, Configure & Deply the Integration Flow

1. Navigate to **Design > Integrations and APIs**.

2. Seach for the package "**Advanced Event Mesh Exercise - Solution**" and select it.

   ![](./images/ex2-4.png)

3. Navigate to the **"Artifacts"** tab select the **"Action"** button and click **"Copy"**

   ![](./images/ex2-5.png)

4. Change the name to **AEM_to_REST_EventMediation_UserXXX** and replace **XXX** with your assigned user number. Press the **"Select"** button to select the package.

   ![](./images/ex2-6.png)

5. Select the package you created in Exercise 2.2.

   ![](./images/ex2-7.png)

6. Press **"Copy"** button

   ![](./images/ex2-8.png)

7. Press **Navigate** to go directly to the copied package.
<br>![](./images/ex2-9.png)

8. Click on the copied integration flow to open it.
   ![](./images/ex2-10.png)

9. The integration flow will subscribe to your queue and performs a simple transformation from JSON to XML format. The result is sent to the HTTP reciever endpoint that you created in Exercise 2.1. Press **Configure** to set the required properties.

    ![](./images/ex2-11.png)

10. Provide the name of your AEM queue that you created in Exercise 1: **User_XXX** (replace **XXX** with your assigned user number).

    ![](./images/ex2-12.png)

11. Switch to the **"Receiver"** tab and provide your unique webhook URL you created in Exercise 2.1 and click on **"Save"** button.

    ![](./images/ex2-13.png)

12. **Close** the warning message.

    ![](./images/ex2-14.png)

13. Press **"Deploy"** to deploy your integration flow.

    ![](./images/ex2-15.png)

14. Select Runtime Profile **"Cloud Integration"** and press **"Yes"**. Press **"Ok**" to close the dialog.

    ![](./images/ex2-16.png)


## Exercise 2.4: Configure Standalone Web Application as Second Subscriber
In this exercise you will configure the Business Partner Web Application. On this Website you will subscribe to the queue created in Exercise 2.1 via your web browser. Every business partner change published to your queue will be shown on the web application in real-time.

1. Open the [Business Partner Web Applicaiton](https://sap-cpisuite-europe-01n-cpisuite-europe-01-aem-demo-client.cfapps.eu10.hana.ondemand.com/app/index.html#/businessPartner).
2. Provide the same connection details as captured in [Exercise 1.4 - Send an event from the Try Me! Tool to your Topic](../ex1#exercise-14---send-an-event-from-the-try-me-tool-to-your-topic)
3. Change Subscription Type to **"Queue"** and fill in the queue name created in Exercise 2.1: **User_XXX_WebApp** (replace **XXX** with your assigned user number). Press **"Connect"**.

	> **_HINT:_** If your broswer is asking to use a certificate for authentication, press "Do not send certificate".

	![Pic](./images/ex3-5.png)

4. The Pop-Up should close and status shows **"Connected"**. Now your browser is directly subscribed to the queue and ready to receive business partner events.

   ![Pic](./images/ex3-6.png)

## Exercise 2.5: Run the scenario by publishing the RAP-based S/4 HANA Business Partner Change event, which involves modifying an existing business partner
In this exercise we will publish a Business Partner Change event in S/4Hana that will trigger both the subscribers automatically.

1. **Access T41** : Open SAP GUI from WTS
   <br>Link: https://class.learning.sap.com/my.policy
   <br>System : **SY-S42023FPS2BGACC-WS001**
   <br>Username : **WS-XXX** where **XXX** is your assigned user number
   <br>Password: provided by the moderator
   
   **Note:** In case you get the error that **"Your session could not be established."**, open a new session

   ![](assets/20250818_233959_image.png)
   <br><br>![](assets/20250818_234051_image.png)

2. Open SAP Logon and click on T41

      ![](assets/20250818_234756_image.png)

3. Give User: **S4F17-XX** where **XX** is the assigned user number. Example -> S4F17-01
   <br>Password: **Welcome1**

   Click **"Enter"**

   ![](assets/20250818_234838_image.png)

4. Accept the system messages

   ![](assets/20250818_234850_image.png)

5. Training Desktop will be open as given below:

   ![](assets/20250818_234917_image.png)

6. Enter Tcode: /nbp and click on enter button.

   ![](assets/20250819_002227_image.png)

7. Enter Business Partner number **S610-AXX** where **XX** is your assigned user number
   Click on "Start"

   ![](assets/20250819_002301_image.png)

8. Choose the Business Partner by double clicking.

   **Note: In the screenshots, we are using 01 group as an example**

   ![](assets/20250819_002331_image.png)

9. Click on **Change** button as highlighted below.

   ![](assets/20250819_002352_image.png)

10. Change details of the Business Partner such as name.

    ![](assets/20250819_002439_image.png)

11. Click on **"Save"**

    ![](assets/20250819_002458_image.png)

12. Enter **/n/IWXBE/EVENT_MONITOR** t-code to view the monitoring.

    ![](assets/20250819_002523_image.png)

13. Click on **AEM_BASIC_RAP**

    ![](assets/20250819_002542_image.png)

14. Click on outbound events. Check the event triggered for your group number by the topic name:

    **s4/t41/400/ce/groupXX/BusinessPartner/Changed/v1** where **XX** is your assigned user number

    **In our example for group01 - "s4/t41/400/ce/group01/BusinessPartner/Changed/v1"**

    ![](assets/20250819_002612_image.png)

15. You can see all messages including the payloads

    ![](assets/20250819_002635_image.png)

### Exercise 2.5.1. Monitor Consumed Messages
As S/4 Hana system published an event to a topic, all queues subscribed to that topic have received the event. This means the integration flow configured in Exercise 2.3 is executed and also the standalone web application should have received the event.

1. Navigate to "**Monitor-> Integrations and APIs**". Open the **"Manage Integration Content"** tile.

    ![](./images/ex2-17.png)

2. Search for your integration flow. It should be in **"Started"** status. Press **"Monitor Message Processing"** to view the processed Messages.

    ![](./images/ex2-18.png)

3. You should see at least one Messages in the list with Status **"Completed"**.

   ![](./images/ex2-19.png)

4. Open the webhook site created in Exercise 2.1. Here you should the messages sent from Cloud Integration. Notice the enriched payload by the integration flow callback to the event publisher.

   ![](./images/ex2-20.png)

5. You should also see your entry in the standalone web application. Be aware that if you send a business partner with the same ID, an update of the existing entry will be triggered instead of creating a new entry.

   ![Pic](./images/ex3-8.png)
   
**Congratulations, you have completed all the exercises!**
