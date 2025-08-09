+++
title = "Creating Denied Topics"
date = 2024-05-14T00:38:32+07:00
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

Guardrails can be configured with a set of denied topics that are undesirable in the context of your generative AI application. For example, a bank may want their AI assistant to avoid any conversation related to investment advice or engage in conversations related to cyrptocurrencies.

You can define up to 30 denied topics. Input prompts and model completions will be evaluated against each of these denied topics. If one of the denied topics is detected, the blocked message configured as part of the guardrail will be returned to the user.

Denied topics can be defined by providing a natural language definition of the topic along with a few optional example phrases of the topic. The definition and example phrases are used to detect if an input prompt or a model completion belongs to the topic.

In the following section we will configure three types of Denied topics for m**edical advice**, **financial advice** and **political advice**.
