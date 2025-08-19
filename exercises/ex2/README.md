## Exercise 2 - Use Cloud Integration capablity for event mediation
In this exercise, an Integration Flow is added as a consumer via the Advanced Event Mesh adapter using the Solace Messaging Format (SMF). Integration flows can be used to mediate events, such as mapping of event structures and data, enriching event payloads (for example, catching a narrow business notification event and calling back to the event publisher to enrich with more data)

## Exercise 2.1 - Setup REST Endpoint

Before we start building our integration flow, we will "provision" a simple HTTP endpoint where we will send the message.

1. ### Webhook.site (HTTP endpoint)

    For simplicity purposes, our REST consumer will be a simple HTTP endpoint that will receive the messages from the queue. We will use a tool called [Webhook.site](https://webhook.site/) to create a temporary endpoint that will receive the messages. When you navigate to the website, you will be presented with a unique URL that you can use to receive the messages. **Take note of the unique URL** as we will use it to configure the REST consumer.
    
    <p align = "center">
        <img alt="webhook.site example" src="images/webhook-site-example.png" width="100%"/><br/>
        <i>webhook.site example</i>
    </p>

## Exercise 2.2 - Create Integration Package in Cloud Integration capability of SAP Integration Suite

1. Open the SAP Integration Suite landing page via this [link](https://cpisuite-europe-03.integrationsuite.cfapps.eu20-001.hana.ondemand.com/shell/home).

   ![](./images/ex2-1.png)

2. Navigate to **Design > Integrations and APIs**, and select **Create**.

   ![](./images/ex2-2.png)
   
3. Fill the following:
   <br>**Name:** "User**XXX**" where **XXX** is your assigned user number
   <br>**Short Description:** "Integration Package for event mediation from User **XXX**".

   <br>click **Save**.

   ![](./images/ex2-3.png)

## Exercise 2.3 - Copy & Configure the Subscriber Integration Flow

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

9. The integration flow will subscribe to your queue and performs a call back to the event publisher to enrich with more data (Mock API Call). The result is sent to the HTTP reciever endpoint that you created in Exercise 2.1. Press **Configure** to set the required properties.

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


## Exercise 2.4. Monitor Consumed Messages
1. Navigate to "**Monitor-> Integrations and APIs**". Open the **"Manage Integration Content"** tile.

    ![](./images/ex2-17.png)

2. Search for your integration flow. It should be in **"Started"** status. Press **"Monitor Message Processing"** to view the processed Messages.

    ![](./images/ex2-18.png)

3. You should see at least one Messages in the list with Status **"Completed"**.

   ![](./images/ex2-19.png)

4. Open the webhook site created in Exercise 2.1. Here you should the messages sent from Cloud Integration. Notice the enriched payload by the integration flow callback to the event publisher.

   ![](./images/ex2-20.png)

Please continue with [Exercise 3](../ex3/README.md)
