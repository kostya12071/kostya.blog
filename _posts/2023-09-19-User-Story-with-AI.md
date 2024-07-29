---
title: "Overcoming the User Story Bottleneck: An AI Approach"
excerpt_separator: "<!--more-->"
date: 2023-09-19
categories:
  - Blog
tags:
  - SDLC
  - DevOps
  - AI

---

![AI helping Product Owner with User Stories](/assets/images/ai-ba-hero.png)

Throughout my experience in product delivery, a common challenge I’ve observed is the difficulty business analysts face in crafting comprehensive user stories, especially when product owners have limited availability for initial collaboration. This early bottleneck in the requirements gathering process has a significant impact on team productivity and efficiency.

<!--more-->

Business Analysts (BAs) are left to mind-read what POs want with limited direction. Only later, once stories are complete, can Product Owners (POs) provide feedback—resulting in heavy rework.

Utilizing AI augmentation can effectively eliminate this bottleneck. By harnessing the power of generative AI to extrapolate essential details from the intended requirements, coupled with human oversight, teams can expedite the delivery of well-aligned user stories.

Here is how BA can leverage AI for user stories:

1. First, the BA captures condensed story titles in Jira or Azure DevOps —conveying each need in a few words. 
1. Next, the titles are exported to CSV File
1. Using AI tool like Claude (https://claude.ai/), the BA provides high-level context on the product and target users, any documentation and exported CSV file of user stories titles. With this foundation, Claude drafts multi-paragraph stories for each title. The AI enhances titles with critical functionality, edge case, and UI details—work that would take a BA hours.
1. The BA imports AI draft stories into Jira to refine as needed before presenting to PO. The goal is a complete set of stories that anticipates PO feedback.
Claude is particularly well-suited for this use case because it supports importing existing story files and requirement documents directly; instead, you’ll need to manually copy and paste the content into the chat window if you decide to use ChatGPT. This unique feature is why I favor using Claude AI.

## Detailed Instructions

### Step 1. Create stories in DevOps

Using Azure DevOps, Jira or a tool of your choice, create a list of User Stories completing the title only, describing the requirement in few words.

![Azure DevOps User Stories](/assets/images/Step1-Create-User-Stories-Titles.png)

### Step 2: Export Stories from Azure DevOps to CSV

Configure the following columns in the export file:

- ID
- Work Item Type
- Title
- Description

![Selecting column options in Azure DevOps](/assets/images/Step3-Export-Columns.png)

![Configure Query in Azure DevOps](/assets/images/Step2-Export-Backlog-Items.png)

### Step 3: Asking AI for Help

This process can be divided into two distinct steps. The first step involves identifying any issues within the initial set of requirements, while the second step focuses on expanding and providing more details for the user stories.

In Claude AI: 

Sample prompt (replace with your product details) and attach the CSV file

> I am developing a mobile app and a web service for a Timing Application. The application must be intuitive to use, 
> provide accurate timing, and have features that coaches would find useful. The primary users of this app would be coaches for cross-country and track and field events.
> Attached is the Product backlog for this application. Please review the items for duplicate requirements or missing requirements. Provide a bulleted list of recommendations.
- prompt

Review the feedback, return to the Backlog tool to implement the necessary changes, and then proceed to re-export the updated list as a CSV file.

User Story Expanding Prompt

> The updated backlog is attached. Please create detailed user stories for each backlog item on the list based on 
> the provided title and your understanding of the application context.  Detailed user stories should be populated as Description columns. Be as detailed as possible and include the expected 
> behavior, alternative flows, possible edge cases to consider. Also include any details on the UX/UI, if appropriate.
> Generate the list as exportable CSV with the following properties:
> Columns as State,ID,Work Item Type,Title,Description
> All data types are string type and should be in quotes
- prompt

If you notice that the output gets truncated, it is probably because AI runs into an output character limit.  The maximum response size for Claude AI is around 3000 words. This means that the model’s generated response, including both text and spaces, should not exceed this limit.  If this occurs, simply ask Claude AI to continue:

> please continue where you left off
- prompt

Example User Stories that AI came up with:

**Display Timer**

As the user, when I start a timer, it displays prominently on screen with a large font for elapsed time that refreshes every second. Controls to Start, Stop and Reset the timer are visible below the time. If I try to navigate away from the page during an active timer, a warning message prompts me to confirm leaving the page so no timing is missed accidentally.

**Stop a Running Timer**

As a user with a timer in progress, I can click/tap the Stop button below the timer to immediately pause timing. The digits change color to indicate stopped state. I can also resume a stopped timer. If I try stopping an inactive timer, it shows a warning the timer is not currently running.

ai response

### Step 4: Import Stories into to DevOps

Copy output from Claude AI into a text file using your favorite text editor (VS Code or Notepad ++ are great options). Make sure you remove any content before the heading row as well any trailing spaces after the last “ on each line.

Files should look like this 

![CSV file example](/assets/images/Step5-Save-CSV-AI-Output.png)
Import work items in the Queries window on Azure DevOps.

![Azure DevOps import work items](/assets/images/Step6-Import-CSV.png)

If you receive an error “There were issues while importing this CSV file "double-quoted value possibly terminated too early or missing delimiter at line x ,column y". you probably have trailing spaces on some of your lines in CSV.  To remove the trailing spaces you can use Visual Studio Code or Notepad++

```
Ctrl+K, Ctrl+X in Visual Studio

Alt + Shift + S in Notepad++
```

![Issues while importing this CVS file on Azure DevOps](/assets/images/Error-Import.png)

I hope you find this information useful if you have any additional feedback suggestions or can share your experience using these tools please let me know

The result? Requirements time cut 50%+ across teams. BAs write less, advise more. POs get aligned stories faster without extensive hand-holding.

The key is balancing AI’s untiring drafting with human insight. Together they overcome early process bottlenecks. Teams gain accelerated delivery and delighted stakeholders.

Does your team use AI to enhance agile requirements? Please share your lessons learned in the comments.

### Security Note

It is crucial to recognize that numerous enterprises and government agencies have stringent restrictions in place concerning the transmission of company-confidential data to publicly accessible services, including Claude AI. Furthermore, certain companies may have specific policies governing the use of AI technologies. Therefore, before sharing any data with a third-party service, it is imperative to thoroughly assess and ensure compliance with your organization’s policies and regulations.

As an alternative, consider exploring the Azure Open AI Service for Business, which offers significantly better privacy and security terms tailored to meet business needs, while still enabling you to achieve similar results.