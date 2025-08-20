## Exercise 3: Incremental growth: Add web application as additional consumer

The publish-subscribe pattern decouples the sending and receiving applications. This makes it easy to add new applications allows for incremental growth. In this exercise a web application is added as additional consumer. The web application is subscribed to a queue and lists all business partners.

## Exercise 3.1: Create new queue for RAP based events

1. Go back to the original tab in your browser of AEM and click on **"Cluster Manager"** on the left.
2. In the All Services screen click on the **"Broker Asia"** tile.

> **_HINT:_** If you cannot see the tiles, uncheck the "Only show my services" box.

![](./images/ex3-1.png)

3. Switch to **"Manage"** tab and click on the **"Queues""** tile. A new window opens up.

![Pic](./images/ex3-2.png)

4. Click on Queue to create new queue

   ![](assets/20250818_232239_image.png)
5. Give the Name in the Format
   RAP*AEM*## (where ## is Your Group Number)

   ![](assets/20250818_232519_image.png)
6. Click on "Create" ->Then click on "Apply"

   ![](assets/20250818_232643_image.png)
7. Click on the Queue that is created - Select the Subscription Tab

   ![](assets/20250818_232722_image.png)
8. Enter the Topic name with the below format(Replace ## with Group name)
   s4/t41/400/ce/group##/BusinessPartner/Changed/v1

   ![](assets/20250818_232811_image.png)
9. Click on "Create"

## Exercise 3.2: RAP based events

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

5. ###### **Trigger the RAP event by changing an existing partner**


   1. **Access T41** : Open SAP GUI from WTS link for WTS: https://class.learning.sap.com/my.policy
      Enter the below details
      system:     SY-S42023FPS2BGACC-WS001
      user:       WS-001  till WS-030
      password:   SIXTrainingWS25!

      ![](assets/20250818_234334_image.png)
   2. Open SAP Logon and click on T41

      ![](assets/20250818_234756_image.png)
   3. Give user: S4F17-##   (##-- group number)  Example ->S4F17-01

      password : Welcome1

      Click "Enter"

      ![](assets/20250818_234838_image.png)
   4. Accept the system messages
      ![](assets/20250818_234850_image.png)
   5. Training Desktop will be open as below

      ![](assets/20250818_234917_image.png)
   6. Enter Tcode: /nbp and click on enter button.

      ![](assets/20250819_002227_image.png)
   7. Enter Business Partner number S610-A##((where ## is your group number)
      Click on "Start"

      ![](assets/20250819_002301_image.png)
   8. Choose the Business Partner bydouble clicking.

      **Note: In the screenshots, weare using 01 group for example**

      ![](assets/20250819_002331_image.png)
   9. Click on Change button as highlighted below.

      ![](assets/20250819_002352_image.png)
   10. Change details from the business partner such as name.

       ![](assets/20250819_002439_image.png)
   11. Click on "Save"

       ![](assets/20250819_002458_image.png)
   12. Enter /n/IWXBE/EVENT_MONITOR t-code to view the monitoring.

       ![](assets/20250819_002523_image.png)
   13. Click on AEM_BASIC_RAP

       ![](assets/20250819_002542_image.png)
   14. Click on outbound events. Check the event triggered for your group number by the topic name:

       **s4/t41/400/ce/group##/BusinessPartner/Changed/v1  ( ## your group number ) **

       **In our example for group01**

       **s4/t41/400/ce/group01/BusinessPartner/Changed/v1**

       ![](assets/20250819_002612_image.png)
   15. You can see all messages including the payloads

       ![](assets/20250819_002635_image.png)
6. ###### Check the event which has reached Advanced Event Mesh


   1. Go back to tab in your browser of AEM and click on **"Cluster Manager"** on the left.

      ![](assets/20250819_003214_image.png)
   2. Click on "Broker Asia" broker - in which we created queue and topic subscriptions.
      Click on manage and go to queues.

      Select the queue RAP*AEM*## (where ## is your group number)

      ![](assets/20250819_003428_image.png)
   3. Click on Messages Queued to view the message in AEM

      ![](assets/20250819_003458_image.png)

## Exercise 3.3: Configure Web Application

In this exercise you will conifugre the Business Partner Web Application. On this Website you will subscribe to the queue creatd in exercise 3.1 via your web browser. Every business partner published to your queue will be shown on the website.

1. Open the [Business Partner Web Applicaiton](https://sap-cpisuite-europe-01n-cpisuite-europe-01-aem-demo-client.cfapps.eu10.hana.ondemand.com/app/index.html#/businessPartner).
2. Provide the same connection details as captured in [Exercise 1.4 - Send an event from the Try Me! Tool to your Topic](../ex1#exercise-14---send-an-event-from-the-try-me-tool-to-your-topic)
3. Change Subscription Type to **"Queue"** an fill in the queue name created in exercise 3.1: **User_XXX_WebApp** (replace **XXX** with your user number). Press **"Connect"**.

> **_HINT:_** If your broswer is asking to use a certificate for authentication, press "Do not send certificate".

![Pic](./images/ex3-5.png)

5. The Pop-Up should close and status shows **"Connected"**. Now your browser is directly subscribed to the queue and ready to receive business partner events.
   ![Pic](./images/ex3-6.png)

## Exercise 3.4: Publish RAP based event again

1. To publish an S4 RAP based events - Repeat [Excercise 3.2.3 Steps 1 - 11](exercises/ex3#trigger-the-rap-event-by-changing-an-existing-partner)
2. You should see your entry in the application. Be aware that if you send a business partner with the same ID, an update of the existing entry will be triggered instead of creating a new entry.
   ![Pic](./images/ex3-8.png)
3. As system published the event to a topic, all queues subscribed have received the event. This means also the integration flow in exercise 2 is executed again and you should see an corresponding entry in the webhook site.

**Congratulations, you completed all exercises!**
