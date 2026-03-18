---
title: "From Research Paper to Prototype: Using Generative AI to Automatically Generate Test Cases"
date: 2026-03-15
description: "How a 5-year-old IEEE research paper on Search-Based Software Testing (SBST) became a practical reality through Generative AI and AWS Bedrock."
tags: ["Generative AI", "LLM", "AWS Bedrock", "Software Testing", "Serverless", "QA"]
categories: ["Engineering", "AI"]

cover:
  image: "ai-sbst-cover.png"
  alt: "Conceptual visualization comparing research on mathematical optimization with modern AI semantic reasoning for test generation."
  caption: "Yesterday’s theoretical research meets today's practical tools: visualizing the shift from mathematical optimization to AI semantic reasoning."
---

## Introduction

About five years ago, I came across a research paper on **Search-Based Software Testing (SBST)** published on IEEE.

The idea was fascinating: instead of writing test cases manually, software testing could be treated as an optimization problem. Algorithms could explore the space of possible inputs and automatically discover test cases that maximize coverage and expose hidden defects.

Conceptually, it felt like a glimpse into the future of testing.

**But there was a problem.**

While the theory was elegant, turning it into something practical was difficult. Implementing SBST systems required complex tooling, specialized algorithms, and infrastructure that most development teams simply did not have access to.

At the time, the idea stayed in the back of my mind as an interesting possibility that felt just out of reach.

Fast forward several years, and the landscape of software engineering has changed dramatically. While my recent work has focused on mobile architecture and behavioral consistency, this experiment explores how generative AI can improve software testing workflows. With the rise of modern generative AI and large language models (LLMs), machines can now interpret natural language requirements, reason about system behavior, and generate structured outputs.

Suddenly, that old research idea started to feel much more practical.

> **The Shift:** Traditional SBST relied on evolutionary algorithms and mathematical optimization to explore a system's input space. Modern LLMs approach the problem via **semantic reasoning**—interpreting natural language specifications to infer behaviors. Rather than searching blindly for edge cases, AI can now reason about them directly from the requirements.

When an internal innovation summit provided an opportunity to experiment, I decided to revisit that curiosity:

**Could generative AI finally make automated test case generation practical?**

---

## The Problem: Manual Test Case Generation

In many software teams, writing manual test cases remains a time-consuming and repetitive activity. Test engineers often begin with requirements or user stories written in formats such as **Given–When–Then**.

For example:

* **Given** a policyholder submits a claim  
* **When** the claim amount exceeds the policy limit  
* **Then** the claim should be rejected  

While this format improves readability, it often leaves several important questions unanswered:

* What edge cases exist?
* Are boundary conditions clearly defined?
* What negative scenarios should be tested?
* Are there missing requirements or ambiguous behaviors?

As a result, QA engineers must manually expand each user story into a comprehensive set of test scenarios.

This process is valuable but slow—and it is exactly the type of structured reasoning that modern AI models excel at.

---

## The Idea: AI-Assisted Test Case Generation

The core idea behind my prototype was simple: **use generative AI to analyze user stories and automatically produce detailed manual test cases.**

The system takes user stories written in **Given–When–Then** format and generates:

1. **Detailed test scenarios**
2. **Step-by-step execution instructions**
3. **Expected results**
4. **Edge cases**
5. **Potential gaps or anomalies in the specification**

---

## Architecture Overview

To implement the prototype quickly and avoid infrastructure overhead, I built the system using a **serverless architecture on AWS**.


```
[ Client Application ] ──▶ [ API Gateway ] ──▶ [ AWS Lambda ] ──▶ [ Amazon Bedrock ] ──▶ [ Jurassic-2 Ultra ]
```


### AWS Lambda: The Core Processing Engine

The backbone of the system is an AWS Lambda function responsible for:

- Receiving API requests
- Formatting prompts for the AI model
- Sending requests to Amazon Bedrock
- Processing and returning generated test cases

The serverless model allowed me to focus on application logic rather than infrastructure management.

---

### Amazon Bedrock: Managed Generative AI

Amazon Bedrock provides a **managed interface for accessing foundation models** without the need to manage model infrastructure.

For this prototype, I selected **AI21 Jurassic-2 Ultra**, which at the time of the proof-of-concept demonstrated strong **instruction-following capabilities** and produced consistently structured outputs suitable for generating test scenarios.

---

### Prompt Design: The Key to Results

Rather than simply asking the model to generate tests, the prompt provided structured instructions describing the expected output format.

The model was guided to:

- identify requirement gaps
- generate boundary scenarios
- produce structured test steps and expected outcomes

In practice, the prompt acted as a **lightweight specification** that steered the model toward more structured reasoning.

---

## Example Output

Given the earlier user story regarding policy claims, the AI generated the following scenarios:

### Test Case — Claim Exceeds Policy Limit

**Steps**

1. Submit a claim greater than the maximum policy coverage.
2. Process claim through validation system.

**Expected Result**

The system rejects the claim and displays an appropriate error message.

---

### Test Case — Boundary Condition

**Steps**

1. Submit a claim exactly equal to the policy limit.

**Expected Result**

The claim should be approved.

---

> ### 🤖 AI Observation: Requirement Gap Detection
> **Observation:** The specification does not clarify whether partial approvals are allowed if the claim exceeds the policy limit.
>
> **Suggested Clarification:** Define whether the system should automatically adjust the payout to the maximum allowed value.

This type of analysis can help identify **requirement gaps early in the development cycle**.

---

## The Bigger Opportunity for QA

The goal of this prototype is not to replace QA engineers.

Instead, it demonstrates how generative AI can augment the testing process by:

* **Accelerating** test case generation
* **Identifying** requirement gaps earlier
* **Improving** coverage of edge cases
* **Reducing** repetitive manual work

This aligns with the **shift-left testing** movement, where quality assurance begins earlier in the development lifecycle.

However, like any AI-assisted workflow, generated test cases should be treated as **suggestions rather than authoritative outputs**. A **human-in-the-loop** remains essential to validate scenarios and ensure they align with the intended system behavior.

---

## Future Directions

While this prototype focused on manual test cases, several extensions are possible:

* Integration with issue tracking systems such as **Jira**
* Automatic generation of **automated test scripts** (Selenium, XCTest)
* Continuous analysis of specifications for inconsistencies

Beyond manual scenarios, a natural evolution is generating **unit tests directly from source code**.

By analyzing execution paths and boundary conditions, generative AI can help bridge the gap between high-level requirements and low-level code coverage—a topic I plan to explore in a future article.

---

## Final Thoughts

Sometimes ideas arrive before the tools needed to realize them.

What began as a curiosity sparked by a research paper eventually became a practical experiment made possible by the convergence of **serverless computing and foundation models**.

For me, this project was a reminder that the most interesting engineering experiments often begin with a simple question:

**What becomes possible when yesterday’s research finally meets the tools capable of bringing it to life?**

---
### Cross-platform Links
**Also published on:**
* **DEV Community:** [From Research Paper to Prototype](https://dev.to/pavan-kumar-appannagari/from-research-paper-to-prototype-using-generative-ai-to-automatically-generate-test-cases-418m)
* **Medium:** [From Research Paper to Prototype](https://medium.com/@pavan.kumar.appannagari/from-research-paper-to-prototype-using-generative-ai-to-automatically-generate-test-cases-bd587d894ae5)

---

Written by Pavan Kumar Appannagari — Software Engineer — Mobile Systems & Applied AI



