---
title: "AI Security Skills Challenge - Week 0: Project Setup & Administration"
date: 2025-07-16
draft: false
categories: ["Projects"]
tags: ["Azure DevOps", "GitHub", "Hugo", "Automation", "Documentation"]
---

[Project page](/projects/ai-security-skilling-challenge/index.html)

[GitHub - Week 0](https://github.com/marcusjacobson/Projects/blob/main/Microsoft/Azure%20Ai%20Security%20Skills%20Challenge/00%20-%20Project%20Setup%20%26%20Admin/README.md)

## Week 0 Overview

This week focuses on establishing the foundational infrastructure and workflows for the 12-week AI Security Skills Challenge. The goal is to create a robust project management and documentation ecosystem that will support the entire learning journey.

## Planned Activities

### Project Management Setup

- [X] Set up Azure DevOps project board
- [x] Define sprint structure for 12-week timeline
- [x] Create work items and backlog for each week
- [x] Configure project tracking and reporting

### Documentation Infrastructure

- [x] Initialize GitHub repository structure
- [x] Set up Hugo-based GitHub Pages site
- [x] Create folder structure for prompt library
- [x] Define prompt tagging convention and markdown templates
- [x] Create project scaffolding in portfolio site

### Prompt Library Foundation

- [x] Organize prompt library by domain (Security, Governance, AI Agents)
- [x] Create markdown template for prompt entries
- ~~[ ] Set up Microsoft 365 Copilot Prompt Gallery integration~~
- ~~[ ] Develop PowerShell automation for weekly prompt library backup~~

**Note**: The steps relating to the M365 prompt library are being omitted from the project since I was only able to save prompts to my personal list, with no good way available yet to save a prompt library specific for the project. Therefore GitHub will be the central source of truth for prompts.

## Key Deliverables

### 1. Azure DevOps Project Board

**Status**: [TO BE UPDATED]

- Sprint configuration for 12 weeks
- Work item templates for weekly activities
- Tracking dashboard for progress monitoring

### 2. GitHub Repository Structure

**Status**: [COMPLETE]

```text
Microsoft/Azure Ai Security Skills Challenge/
├── 00 - Project Setup & Admin/          # Week 0 foundation setup
├── 01 - AI-Infused Security Foundations/
├── 02 - Defender XDR + Copilot Integration/
├── 03 - Microsoft Purview for Data Governance/
├── 04 - Microsoft Priva and Responsible AI/
├── 05 - Microsoft Fabric for Secure Analytics/
├── 06 - Copilot Studio for Security Agents/
├── 07 - Azure AI Foundry & Secure AI Workloads/
├── 08 - Customer-Facing AI Solutioning/
├── 09 - AI-First Delivery Practices/
├── 10 - Secure Copilot Deployment Project/
├── 11 - AI Agent Toolkit Project/
├── 12 - Review, Reflect, and Refresh/
├── Prompt-Library/                      # Centralized prompt repository
│   ├── Security/                       # Security-focused prompts
│   ├── Governance/                     # Data governance prompts
│   ├── AI_Agents/                      # AI agent development prompts
│   ├── prompt-template.md              # Standard template
│   └── README.md                       # Library documentation
└── README.md                           # Project overview
```

### 3. Hugo Site Configuration

**Status**: [COMPLETE]

- Theme customization for technical documentation
- Navigation structure for weekly content
- Integration with GitHub Pages deployment
- SEO and analytics configuration

### 4. Prompt Library Infrastructure

**Status**: [COMPLETE (with exceptions)]

- Tagging convention: `[domain]-[scenario]-[complexity]`
- Markdown template with metadata fields
- Search and filtering capabilities
- ~~Automated backup to personal gallery~~

## Lessons Learned

### What Worked Well

The project setup phase matched most of my expectations of how this stage would go. Integrating the AI Security Skills Challenge into my existing Azure DevOps workflow was surprisingly seamless—I was able to slot the 12-week timeline directly into my current sprint planning without disrupting established work patterns. This approach proved that personal learning projects don't have to exist in isolation from professional workflows.

GitHub Copilot emerged as a genuine productivity multiplier during the initial scaffolding phase. Rather than starting from blank templates, I could rapidly generate project structures and README frameworks, then focus my energy on customization and content creation. The most satisfying part  was leveraging Claude Sonnet 4 in agent mode within VS Code to prototype prompt templates as well as a threat hunting prompt example. Since I was simply using this prompt to test the template, I was able to one-shot the template creation using Ai. Running it a couple of times appeared to provide consistent, meaningful results. For future stages of the project, I will be continuing to use this type of generation for the prompts created in future stages of this project, however I intent to add my own customizations to make sure the prompts behave EXACTLY as I want them to.

Building on my existing Hugo portfolio site architecture was another strategic win. The established category and tagging systems provided immediate content organization capabilities, while the proven deployment pipeline gave me confidence that weekly publications would flow smoothly.

### Challenges Encountered

The Microsoft 365 Copilot prompt library integration hit an unexpected roadblock. While I had envisioned creating a dedicated project workspace for collaborative prompt development, the platform currently limits prompt saves to personal libraries only. This limitation forced a pivot back to GitHub as the single source of truth. In retrospect, this maintains better version control and public accessibility anyway.

### Process Improvements

Week 0 focused on establishing the foundation rather than optimizing existing processes, so the real process insights will emerge as the project matures. However, the integration approach with existing DevOps workflows already suggests that future learning initiatives should leverage established infrastructure rather than creating parallel systems.

## Next Steps

Week 1 will focus on deploying the first set of Microsoft security technologies and beginning the hands-on learning phase. The foundation established this week will enable efficient documentation and knowledge capture throughout the remaining 11 weeks.

### Week 1 Preview

- Microsoft Security Copilot documentation review
- Microsoft Defender for Cloud deployment
- First prompt library entries
- Initial findings publication

## Resources & References

### Project References

- [Prompt library entry template](https://github.com/marcusjacobson/Projects/blob/main/Microsoft/Azure%20Ai%20Security%20Skills%20Challenge/Prompt-Library/prompt-template.md)
- [Prompt Sample](https://github.com/marcusjacobson/Projects/blob/main/Microsoft/Azure%20Ai%20Security%20Skills%20Challenge/Prompt-Library/Security/SAMPLE-critical-cve-threat-hunting.md)
- [Project home (GitHub)](/projects/ai-security-skilling-challenge/index.html)

### Leveraged Technologies

- [Azure DevOps](https://dev.azure.com)
- [GitHub Pages](https://pages.github.com)
- [Hugo Static Site Generator](https://gohugo.io)

---

*This post is part of the AI Security Skills Challenge series. View the complete [project overview]({{< ref "/projects/ai-security-skilling-challenge" >}}) and follow along with the weekly progress updates.*
