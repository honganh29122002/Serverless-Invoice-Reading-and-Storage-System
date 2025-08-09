+++
title = "Apply Guardrails to Agent"
date = 2020-05-14T00:38:32+07:00
weight = 7
chapter = false
pre = "<b>7. </b>"
+++

Now that these guardrails has been tested, ABCD Bank can create agents and enforce these guardrails on the same.

1. Click on Agents under Builder tools from left of the Amazon Bedrock console page.
   ![img](/images/7/img.png?width=90pc)

2. Click on **"Create Agent"**
   ![img_1](/images/7/img_1.png?width=90pc)

3. (Optional) Change the automatically generated Name for the agent and provide an optional Description for it. Choose **Create**. You will be taken to the Agent builder for your newly created agent, where you can configure your agent.
   ![Agent3](/images/7/Agent3.png?width=90pc)

4. For the Agent resource role, select **"Create and use a new service role"** to let Amazon Bedrock create the service role and set up the required permissions on your behalf.
   ![img_2](/images/7/img_2.png?width=90pc)

5. In the **Select Model** you can choose a model for the agent. Refer here to see the supported models for agents. Within the instructions for the agent, provide the following instructions.

_"You are a customer service representative at ABCD Bank, a leading financial institution. You are friendly, professional, and attentive. Your primary responsibilities include assisting customers with their needs, providing information about products and services, addressing customer inquiries, and ensuring a positive customer experience."_

![Agent5](/images/7/Agent5.png?width=90pc)

6. Scroll down to the **Guardrails details** section, choose **Edit** to associate our guardrail with the agent.
   ![img_3](/images/7/img_3.png?width=90pc)

7. Select our Guardrail and Click on **Save and Exit** to associate our guardrail with the agent. _In case you recieve a message of "You must save your agent with an Agent Resource Role defined before adding a guardrail" then try saving the Agent first before associating the Guardrail_
   ![img_4](/images/7/img_4.png?width=90pc)

8. Click on **Prepare** the agent in order to test it with our updated configurations in the test window.
   ![img_5](/images/7/img_5.png?width=90pc)

9. Now you can test the agent using the same scenarios we selected earlier in the right panel
