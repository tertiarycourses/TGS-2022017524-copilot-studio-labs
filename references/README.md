# Create Copilot Chatbots and Agents with Microsoft Copilot Studio

[![Course](https://img.shields.io/badge/Course-Tertiary%20Courses-blue)](https://www.tertiarycourses.com.sg/wsq-develop-ai-powered-copilots-and-chatbots-with-microsoft-copilot-studio.html)
[![SkillsFuture](https://img.shields.io/badge/SkillsFuture-Funded-green)](https://www.skillsfuture.gov.sg/)
[![Duration](https://img.shields.io/badge/Duration-2%20Days-orange)]()
[![Labs](https://img.shields.io/badge/Labs-16%20Hands--On-purple)]()

> **Register for the course:** [WSQ - Develop AI-Powered Copilots and Chatbots with Microsoft Copilot Studio](https://www.tertiarycourses.com.sg/wsq-develop-ai-powered-copilots-and-chatbots-with-microsoft-copilot-studio.html)

This repository contains hands-on lab materials for the **WSQ - Develop Intelligent Chatbots with Microsoft Copilot Studio and Generative AI** course. Learn to build AI-powered chatbots and agents using Microsoft Copilot Studio, from fundamentals to advanced multi-agent systems.

## Course Overview

| Aspect | Details |
|--------|---------|
| **Duration** | 2 Days (9:30 AM - 6:30 PM) |
| **Mode** | Physical / Zoom / On-site Corporate |
| **Certification** | Certificate of Completion + SkillsFuture OpenCert |
| **Course Code** | TGS-2022017524 |

## Learning Outcomes

Upon completion, you will be able to:

- Map out chatbot storyboards to suit customer preferences
- Determine appropriate chatbot content frequency and delivery types
- Select optimal deployment channels and assess chatbot performance
- Build conversational AI agents using Microsoft Copilot Studio
- Integrate generative AI and Power Automate for automation
- Deploy agents across multiple channels (Teams, M365 Copilot, Web)

---

## Labs Structure

### Day 1: Foundations & Core Concepts (Labs 1-11)

Build your foundation in Copilot Studio with these progressive labs covering agent creation, knowledge grounding, topics, Power Automate flows, and testing.

| Lab | Title | Description |
|-----|-------|-------------|
| **Lab 1** | [Introduction to Agents](Day%201/Lab%201/index.md) | Learn foundational AI concepts: LLMs, RAG, conversational vs autonomous agents |
| **Lab 2** | [Copilot Studio Fundamentals](Day%201/Lab%202/index.md) | Explore the four building blocks: Knowledge, Tools, Topics, and Instructions |
| **Lab 3** | [Deploy a Declarative Agent for M365 Copilot](Day%201/Lab%203/index.md) | Build and publish a declarative agent with prompts for Microsoft 365 Copilot |
| **Lab 4** | [Creating a Solution for Your Agent](Day%201/Lab%204/index.md) | Learn Power Platform solutions, publishers, and ALM practices |
| **Lab 5** | [Using a Pre-Built Agent](Day%201/Lab%205/index.md) | Deploy and customize the Safe Travels pre-built agent template |
| **Lab 6** | [Create a Custom Agent Using Natural Language](Day%201/Lab%206/index.md) | Build a Sales Agent with multiple knowledge sources |
| **Lab 7** | [Add New Topic with Trigger and Nodes](Day%201/Lab%207/index.md) | Create topics with triggers, SharePoint connectors, and Power Fx |
| **Lab 8** | [Add Power Automate Flows](Day%201/Lab%208/index.md) | Create agent flows for document and email automation |
| **Lab 9** | [Create Additional Topics with Adaptive Cards](Day%201/Lab%209/index.md) | Build multi-topic agents with price calculator functionality |
| **Lab 10** | [Add Conditional Logic and Branching](Day%201/Lab%2010/index.md) | Implement multi-path conversations with Yes/No conditions |
| **Lab 11** | [Test Your Agent](Day%201/Lab%2011/index.md) | Comprehensive testing and validation before publishing |

### Day 2: Advanced Agent Development (Labs 12-16)

Take your skills to the next level with advanced scenarios including hiring workflows, multi-agent systems, autonomous triggers, and Teams integration.

| Lab | Title | Description |
|-----|-------|-------------|
| **Lab 12** | [Build a Hiring Agent](Day%202/Lab%2012/index.md) | Create a recruitment workflow with eligibility conditions and HR notifications |
| **Lab 13** | [Multi-Agent Systems: Customer Service](Day%202/Lab%2013/index.md) | Build parent-child agent architecture for air fryer customer support |
| **Lab 14** | [Topics and Conversation Flows in Multi-Agent Systems](Day%202/Lab%2014/index.md) | Design adaptive cards and agent routing for customer enquiries |
| **Lab 15** | [Autonomous Hiring Agent with Event Triggers](Day%202/Lab%2015/index.md) | Create event-driven resume processing with email triggers |
| **Lab 16** | [Advanced Hiring Agent Features](Day%202/Lab%2016/index.md) | Add child agents, knowledge sources, and Teams integration for candidate ranking |

---

## Repository Structure

```
copilot-studio-labs/
├── README.md
├── Day 1/                          # Foundations & Core Concepts
│   ├── Lab 1/                      # Introduction to Agents
│   ├── Lab 2/                      # Copilot Studio Fundamentals
│   ├── Lab 3/                      # Declarative Agent for M365
│   │   └── Assets/
│   ├── Lab 4/                      # Creating a Solution
│   │   └── Assets/
│   ├── Lab 5/                      # Pre-Built Agents
│   │   └── assets/
│   ├── Lab 6/                      # Custom Agent (Natural Language)
│   │   └── Assets/
│   ├── Lab 7/                      # Topics with Triggers
│   │   └── Assets/
│   ├── Lab 8/                      # Power Automate Flows
│   │   └── Assets/
│   ├── Lab 9/                      # Additional Topics & Adaptive Cards
│   │   └── Assets/
│   ├── Lab 10/                     # Conditional Logic
│   │   └── Assets/
│   └── Lab 11/                     # Testing
│       └── Assets/
│
└── Day 2/                          # Advanced Agent Development
    ├── Lab 12/                     # Hiring Agent
    │   └── Assets/
    ├── Lab 13/                     # Multi-Agent Systems
    │   ├── Assets/
    │   └── Documents/              # Air fryer product PDFs
    ├── Lab 14/                     # Multi-Agent Topics & Flows
    │   └── Assets/
    ├── Lab 15/                     # Autonomous Event Triggers
    │   └── Assets/
    └── Lab 16/                     # Advanced Hiring Features
        └── Assets/
```

---

## Prerequisites

Before starting the labs, ensure you have:

- [ ] Microsoft 365 account with Copilot Studio access
- [ ] Power Platform environment (Developer or Trial)
- [ ] Microsoft Teams access
- [ ] SharePoint site for lab exercises
- [ ] Basic understanding of conversational AI concepts

### Environment Setup

1. **Create a Developer Environment**: Follow [Lab 4](Day%201/Lab%204/index.md) for detailed setup instructions
2. **Obtain Copilot Studio License**: Trial licenses available at [Copilot Studio](https://copilotstudio.microsoft.com)
3. **Prepare SharePoint Site**: Create a SharePoint site with sample lists for the scenarios

---

## Key Resources

### Microsoft Documentation
- [Microsoft Copilot Studio Documentation](https://learn.microsoft.com/microsoft-copilot-studio/)
- [Power Platform Admin Center](https://admin.powerplatform.microsoft.com/)
- [Copilot Studio Licensing](https://learn.microsoft.com/microsoft-copilot-studio/billing-licensing)

### Learning Paths
- [Build agents with Microsoft Copilot Studio](https://learn.microsoft.com/training/paths/build-agents-copilot-studio/)
- [Make your agent autonomous](https://learn.microsoft.com/training/modules/autonomous-agents-online-workshop/)

### Community Resources
- [Microsoft Agent Academy](https://github.com/microsoft/agent-academy)
- [Power Platform Community](https://powerusers.microsoft.com/)

---

## Course Information

**Provider**: [Tertiary Courses](https://www.tertiarycourses.com.sg/wsq-develop-ai-powered-copilots-and-chatbots-with-microsoft-copilot-studio.html)

**Funding Available**:
- SkillsFuture Credit (SFC)
- SkillsFuture Enterprise Credit (SFEC)
- Post-Secondary Education Account (PSEA)

---

## License

This repository contains lab materials adapted from the [Microsoft Agent Academy](https://github.com/microsoft/agent-academy) and is intended for educational purposes.

---

## Acknowledgments

- [Microsoft Agent Academy](https://github.com/microsoft/agent-academy) for the original lab content
- [Tertiary Courses](https://www.tertiarycourses.com.sg/) for course facilitation
- Microsoft Copilot Studio team for the platform and documentation
