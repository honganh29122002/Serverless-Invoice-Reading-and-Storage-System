+++
title = "Add filters to Guardrail"
date = 2024-05-14T00:38:32+07:00
weight = 5
chapter = false
pre = "<b>5. </b>"
+++

1. In this section you can add optional word filters that you do not want in user inputs or the model responses.

It is recommended to check the **"Profanity Filter"** to ensure that no abusive words can be used during customer interactions
![WordFilter1](/images/5/WordFilter1.png?width=90pc)

Word filters can be used to block specific words and phrases in both input prompts and model responses. These filters are essential for maintaining the integrity, professionalism, and compliance of interactions, especially in sensitive and regulated environments like banking. These can be added manually or uploaded from a list.

Examples That Can Be Used:

- "suicide"
- "self-harm"
- "terrorist"
- "illegal"

Add these words and click Next:
![img](/images/5/img.png?width=90pc)

2. Click on Next. We do not have any requirements to define PII so click on next below to reach **Define blocked messaging** section

![img_1](/images/5/img_1.png?width=90pc)

3. Enable optional contextual grounding check and set to default

![img_2](/images/5/img_2.png?width=90pc)

4. Click on **Next**. Review the information and Click on **Create Guardrail** from the bottom of the page.

![FinishCreateGuardrail](/images/5/FinishCreateGuardrail.gif?width=90pc)
