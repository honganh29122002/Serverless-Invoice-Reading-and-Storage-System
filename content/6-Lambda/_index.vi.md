+++
title = "Testing Guardrail"
date = 2020-05-14T00:38:32+07:00
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

Let us now test our created Guardrail to see how well it is working and if it is meeting Stellar Bank’s requirements:

Click on **Bedrock → Guardrails** and choose the Guardrail created
![img](/images/6/img.png?width=90pc)

You will see a screen similar to the below
![img_1](/images/6/img_1.png?width=90pc)

By default, the working draft of the guardrail is used in the test window. To test a different version of the guardrail, choose Working draft at the top of the test window and then select the version.

To select a model, choose **Select model**. You can choose any model that you enabled at the start of the workshop. After you make a choice, select **Apply**. To change the model, choose **Change**.
![img_2](/images/6/img_2.png?width=90pc)

Enter the following prompts in the Prompt and click **Run** to see what responses are generated

### Financial Advice

**Promp:** "Can you suggest some good stocks to invest in right now?"
![img_3](/images/6/img_3.png?width=90pc)

The model returns a response in the Final response box (that may be modified by the guardrail).

If the guardrail blocks or filters the prompt or model response, a message appears under Guardrail check that informs you how many violations the guardrail detected.
![img_4](/images/6/img_4.png?width=90pc)

To view the topics or harmful categories in the prompt or response that were recognized and allowed past the filter or blocked by it, select **View trace**. We can see that our Financial Advice Guardrail was activated to stop this topic from being discussed.

Use the **Prompt** and **Model response** tabs to view the topics or harmful categories that were filtered or blocked by the guardrail.
![img_5](/images/6/img_5.png?width=90pc)

### Political Opinions:

**Prompt:** "What's your stance on the current government policies?"
![img_6](/images/6/img_6.png?width=90pc)

The model returns a response in the Final response box (that may be modified by the guardrail).

If the guardrail blocks or filters the prompt or model response, a message appears under Guardrail check that informs you how many violations the guardrail detected.
![img_7](/images/6/img_7.png?width=90pc)

To view the topics or harmful categories in the prompt or response that were recognized and allowed past the filter or blocked by it, select **View trace**. We can see that our Political Advice Guardrail was activated to stop this topic from being discussed.

Use the **Prompt** and **Model response** tabs to view the topics or harmful categories that were filtered or blocked by the guardrail.
![img_8](/images/6/img_8.png?width=90pc)

### Medical Advice:

**Prompt:** "What should I do to manage my stress levels due to financial issues?"
![img_9](/images/6/img_9.png?width=90pc)

The model returns a response in the Final response box (that may be modified by the guardrail).

If the guardrail blocks or filters the prompt or model response, a message appears under Guardrail check that informs you how many violations the guardrail detected.
![img_10](/images/6/img_10.png?width=90pc)

To view the topics or harmful categories in the prompt or response that were recognized and allowed past the filter or blocked by it, select **View trace**. We can see that our Medical Advice Guardrail was activated to stop this topic from being discussed.

Use the **Prompt** and **Model response** tabs to view the topics or harmful categories that were filtered or blocked by the guardrail.
![img_11](/images/6/img_11.png?width=90pc)
