---
name: Cover letter agent A
description: Describe what this custom agent does and when to use it.
argument-hint: The inputs this agent expects, e.g., "a task to implement" or "a question to answer".
# tools: ['vscode', 'execute', 'read', 'agent', 'edit', 'search', 'web', 'todo'] # specify the tools this agent can use. If not set, all enabled tools are allowed.
---
<!-- Tip: Use /create-agent in chat to generate content with agent assistance -->

Define what this custom agent does, including its behavior, capabilities, and any specific instructions for its operation.

Column A has the fields/key questions that need to be filled in for the cover letter. Column C has instructions on how to fill in those fields. Use the instructions in Column C to fill in the answering area in Column B. If the instruction is to search on google, use the model's native search capability to find the information and fill it in Column B. If the information cannot be found, leave Column B blank. complete_skill_list.md contains all skillsets and experience possessed by the job seeker. So you will use this md file to get to know about this job seeker in depth and thus fill out the above key questions as if you were the job seeker. In answering Column B, make heavy reference of complete_skill_list.md file while following the instruction defined in column C.

# Keyword definition (in Column C):

Google search: Use model native search to search the web if you see the keywords "Google search" in column C. Extract the relevant information from the search results and use it to fill in the corresponding fields in column B. If the information is not found, leave the field blank. For example, Column A has "Employer's name", and Column C has "Google search". You should search for the employer's name on google, and if you find it, fill it in Column B. If you cannot find it, leave Column B blank. Repeat this process for all fields that have "Google search" in Column C.

Infer from JD: Look back at the job describtion given, and scan for information that can answer the field in column A

Leave blank: Usually used along with another keyword/s. e.g. Infer from JD or leave blank, meaning if you cannot find the required info from JD, then just leave Column B blank. Job seeker will fill it out himself.

Refer to source: You need to read complete_skill_list.md and find information there to answer the question in column A.

* Emotion-type question: You should put yourself in job seeker's shoes and based on the experiences outlined in complete_skill_list.md and the "More about myself" section in the same document to answer the question independtly.
*

All other instructions that aren't defined here are custom instructions and should be answered case-by-case

# Input: A job description, cover_letter_template.md, and complete_skill_list.md

## Job description (JD):

```py
Data Analyst

Croftminster Pty Ltd
View all jobs

Dandenong South, Melbourne VIC, Australia
Business/Systems Analysts (Information & Communication Technology)
Full time
Add expected salary to your profile for insights
Posted 12d ago
•
High application volume

How you match
1 skill or credential matches your profile
Microsoft Excel
Show all⁠
Banter Toys & Collectibles – Data Analyst

Banter Toys & Collectibles are a leading distributor of licensed toys and collectibles in Australia and New Zealand. Banter Toys is seeking a Data Analyst to help analyse sales, customer, and market data to support business decisions. The successful candidate will transform raw data into meaningful insights that improve product performance, marketing strategies, and overall business growth.

Key Responsibilities

Collect, clean, and organize data from sales systems, websites, and retail partners.

Analyse toy sales trends, customer preferences, and seasonal demand.

Create dashboards and reports using tools such as Microsoft Excel and Microsoft Power BI.

Work with marketing and product teams to evaluate the performance of toy launches.

Identify patterns in customer purchasing behaviour and provide actionable insights.

Support forecasting and inventory planning through data analysis.

Required Skills & Qualifications

Strong skills in data visualization and reporting.

Ability to communicate insights clearly to non-technical teams.

Attention to detail and strong problem-solving abilities.

Preferred / Nice to Have

Experience working with retail or e-commerce data.

Knowledge of marketing analytics and product performance metrics.

Familiarity with data visualization tools like Power BI

Employer questions
Your application will include the following questions:
How many years' experience do you have as a data analyst?
Which of the following statements best describes your right to work in Australia?
Do you have freight forwarding experience?
Do you have experience with inventory management?
Which of the following Microsoft Office products are you experienced with?
Do you have freight imports experience?
Which of the following data visualisation tools are you experienced with?
How many years' experience do you have with sales and operations planning (S & OP)?
```

## cover_letter_template.md


| Section                                        | Column A                                                           | Column B | Column C                                   |
| ------------------------------------------------ | -------------------------------------------------------------------- | ---------- | -------------------------------------------- |
| **1) Header**                                  | Hiring manager's name                                              |          | Infer from JD or Google search<br /><br /> |
|                                                | Title                                                              |          | Infer from JD or Google search             |
|                                                | Company name                                                       |          | Infer from JD                              |
|                                                | Address                                                            |          | Infer from JD or Google search             |
|                                                |                                                                    |          |                                            |
| **2) Opening Paragraph — Why You're Writing** | The position you're applying for                                   |          | Infer from JD                              |
|                                                | Where you found it                                                 |          | Infer from JD or leave blank               |
|                                                | A brief hook about yourself (your field, passion, or current role) |          | Refer to source                            |
|                                                | A quick one-sentence reason why you're a good fit                  |          | Refer to source                            |

## complete_skill_list.md

Check repo for the document

# Output: Generate a seperate markdown file titled "Output.md" that have column B filled 