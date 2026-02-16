# **GH-300 Exam Cheat Sheet: Domain 2 (Plans & Features)**

**Exam Weight:** 31% (Highest weighted domain)

**Focus:** Plan differentiation, licensing, policy enforcement, enterprise features (Outer Loop), and advanced configurations (MCP, Agents).

## ---

**1\. Plan Architecture & Limits (The Matrix)**

Candidates must instantly map a persona to a plan. Note the addition of **Copilot Pro+** and the specific limits for "Premium Requests."

| Feature / Limit | Free (Individual) | Pro (Individual) | Pro+ (Individual) | Business (Org) | Enterprise (Org) |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **Target Audience** | Students, Trial | Freelancers | **AI Power Users** | Teams/SMBs | Large Orgs |
| **Price** | Free | $10/mo | **$39/mo** | $19/user/mo | $39/user/mo |
| **Code Completions** | 2,000 / month | Unlimited | Unlimited | Unlimited | Unlimited |
| **Premium Requests** | **50 / month** | **300 / month** | **1,500 / month** | Pooled (Org level) | Higher Pool |
| **Model Access** | Standard (GPT-4.1) | Standard \+ GPT-5 mini | **Full Access** (o1, Claude Opus) | Standard | Standard \+ Fine-tuned |
| **IP Indemnity** | ❌ No | ❌ No | ❌ No | **✅ Yes** | **✅ Yes** |
| **Data Retention** | Retention by default | Retention by default | Retention by default | **Zero Retention** | **Zero Retention** |
| **Management** | Personal Settings | Personal Settings | Personal Settings | Org Policies | Ent. Policies |
| **Knowledge Bases** | ❌ No | ❌ No | ❌ No | ❌ No | **✅ Yes** |
| **Chat on GitHub.com** | ❌ No | ❌ No | ❌ No | ❌ No | **✅ Yes** |

### **🔍 Exam Critical Details:**

* **Premium Requests:** Interactions with **Chat, Agents, or Advanced Models** (e.g., o1-preview, Claude 3.5 Sonnet) count as "Premium." Standard "Ghost Text" completions do not count against this limit.1  
* **Student Access:** Verified students get **Copilot Pro** for free, not just the Free plan.1  
* **IP Indemnity:** Only available on **Business** and **Enterprise**. If a freelancer on Pro gets sued for copyright infringement, GitHub does *not* cover them.  
* **Zero Data Retention:** Business/Enterprise plans do *not* retain prompts/snippets for training by default. Individual plans (Free/Pro) *do*, unless the user explicitly opts out in settings.3

## ---

**2\. Enterprise-Grade Features (The "Outer Loop")**

The **Copilot Enterprise** plan extends AI beyond the IDE (Inner Loop) to the GitHub Platform (Outer Loop).

### **2.1 Knowledge Bases (RAG)**

* **Definition:** Collections of Markdown files, documentation, and issues that Copilot uses to ground its answers (Retrieval-Augmented Generation).  
* **Access:** Available **ONLY** in Copilot Enterprise.4  
* **Usage:** A developer chats on GitHub.com and attaches a "Knowledge Base" (e.g., "Company Engineering Standards") to get compliant answers.  
* **Supported Files:** Primarily Markdown (.md) documentation in repositories.5

### **2.2 Pull Request (PR) Summaries**

* **Function:** Automatically analyzes diffs in a PR and generates a summary description and a "Walkthrough" of changes.  
* **Availability:** Copilot Enterprise.7  
* **Exam Trigger:** If a scenario mentions "speeding up code reviews" or "automating change logs," the answer involves PR Summaries on the Enterprise plan.

### **2.3 Remote Codebase Indexing**

* **Problem:** Local IDE indexing is limited by client hardware and checked-out files.  
* **Solution:** Enterprise allows GitHub to index the **entire repository** on the server side (using vector embeddings).8  
* **Benefit:** Enables developers to ask semantic questions about massive monorepos without cloning them locally (@workspace or \#codebase queries).

## ---

**3\. Governance & Administration (The "Admin" Persona)**

### **3.1 Policy: Suggestions Matching Public Code**

This is the most tested policy setting.

* **Risk:** Copilot suggesting code verbatim from a public repo (potentially GPL).  
* **Configuration Options:**  
  * **Allow:** Suggestions are shown. GitHub *may* provide a reference/link to the source license.  
  * **Block:** Suggestions matching \~150 characters of public code are **silently discarded**.9  
* **Precedence:** An Organization Policy overrides an Individual Policy. If the Org says "Block," the user cannot "Allow" it.9

### **3.2 Content Exclusions**

* **Mechanism:** Admins define file paths (e.g., src/secrets/\*, \*\*/.env) to ignore.  
* **Effect:** Copilot will **not** read these files for context and will **not** provide suggestions while these files are active/focused.  
* **Scope:** Configurable at Repository, Organization, or Enterprise levels.8

### **3.3 Audit Logs**

* **Retention:** 180 Days.11  
* **Query:** Filter logs using action:copilot.  
* **Key Events:** Seat assignment (copilot.seat\_assignment\_created), Policy changes (copilot.policy\_update), and "Suggestions matching public code" blocks.11

## ---

**4\. Advanced Capabilities & New Exam Topics**

Recent updates to the exam objectives (GH-300) include these specific technologies.

### **4.1 Model Context Protocol (MCP)**

* **Definition:** An open standard that allows AI models to connect to external data sources and tools securely.  
* **Use Case:** Connecting Copilot to a PostgreSQL database, a Google Drive folder, or an internal API to fetch context.  
* **Architecture:** Replaces ad-hoc integrations. You run an "MCP Server" (local or hosted) that the Copilot client connects to.  
* **Exam Tip:** If a question asks how to let Copilot "read data from our proprietary internal CRM," the answer is likely **Build/Configure an MCP Server**.

### **4.2 Agent Mode & "Mission Control"**

* **Agent Mode:** An autonomous loop where Copilot plans, executes, tests, and iterates on code changes (synchronous collaboration).  
* **Mission Control:** Refers to the "Agents Panel" or dashboard where users can monitor active agent tasks, steer them (redirection), and view history.  
* **Limits:** Heavily consumes **Premium Requests**. Ideal for Pro+ or Enterprise users.2

### **4.3 BYOK (Bring Your Own Key)**

* **Concept:** Allows organizations to use their own Azure OpenAI or OpenAI API keys instead of the shared GitHub capacity.  
* **Usage:** Often used for **GitHub Models** (prototyping) or accessing specific fine-tuned models not available in the standard Copilot pipe.  
* **Benefit:** Bypasses standard rate limits (you pay your provider directly) and ensures data isolation compliance for strict industries.

## ---

**5\. Quick-Fire Scenario Solver**

**Scenario 1: The "Clean Room" Requirement**

* **Req:** Company requires absolute guarantee that no code suggestions come from open source.  
* **Config:** Copilot Business/Enterprise \-\> Policy: **Block Suggestions Matching Public Code**.

**Scenario 2: The "Freelance Power User"**

* **Req:** A contractor uses Agent Mode extensively to refactor legacy apps and keeps hitting limits mid-month.  
* **Config:** Upgrade to **Copilot Pro+** (1,500 premium requests vs 300 on Pro).

**Scenario 3: The "Onboarding" Problem**

* **Req:** New hires need to ask "How do we handle auth?" and get answers based on the company's internal wiki/docs.  
* **Config:** **Copilot Enterprise** \-\> Create a **Knowledge Base** containing the docs repo \-\> User attaches KB in Chat.

**Scenario 4: The "Legal Shield"**

* **Req:** CTO is worried about being sued for copyright infringement by using AI.  
* **Config:** Must verify the organization is on **Copilot Business** or **Enterprise**. (Individual/Pro plans have **NO** indemnity).

## ---

**6\. Keyboard Shortcuts (Visual Studio Code)**

* **Trigger Suggestion:** Alt \+ \\ (Force trigger)  
* **Accept Full:** Tab  
* **Accept Word:** Ctrl \+ \-\> (Cmd \+ \-\> on Mac) \- *Critical for partial acceptance.*  
* **Next Suggestion:** Alt \+ \]  
* **Open Chat:** Ctrl \+ Alt \+ I (Sidebar)  
* **Inline Chat:** Ctrl \+ I (Editor)  
* **Quick Chat:** Ctrl \+ Shift \+ Alt \+ L

## **7\. Slash Commands (The "Prompt Shortcuts")**

| Command | Action | System Behavior |
| :---- | :---- | :---- |
| **/fix** | **Remediate.** | **Analyzes selection \+ compiler errors. Proposes a code fix.** |
| **/explain** | **Analyze.** | **Generates a natural language explanation of the selected code.** |
| **/tests** | **Generate.** | **Scans @workspace for test frameworks (Jest/PyTest) and writes new unit tests.** |
| **/doc** | **Document.** | **Adds JSDoc/Docstrings/Comments to the selected symbol.** |
| **/clear** | **Reset.** | **Wipes the chat context window (crucial for preventing hallucinations from old queries).** |
| **/new** | **Scaffold.** | **Triggers "New Project" workflow (often hands off to Copilot Workspace).** |

#### 

#### **8\. Chat Participants (@) \- The Context Scope**

#### **Invoked with @. These route your query to a specific "Domain Expert" extension.**

| Participant | Scope / Function | Exam Use Case |
| :---- | :---- | :---- |
| **@workspace** | **The Project Codebase. Uses RAG (Retrieval Augmented Generation) to search your open folder/repo.** | **"How does the auth logic work in this project?" (Answer relies on files *not* currently open).** |
| **@vscode** | **The Editor. Knows commands, settings, and UI.** | **"How do I hide the sidebar?" or "Change theme to dark."** |
| **@terminal** | **The Shell. Reads terminal buffer/output.** | **"Explain this build error." (It reads the red error text in the terminal).** |
| **@github** | **The Platform. Searches Issues, PRs, and Discussions.** | **"Are there any open issues about login bugs?"** |
| **@docker / @azure** | **Extensions. Third-party tools (via MCP).** | **"List my running containers."** |

#### 

### **The "Combo" Pattern:** 

#### **The most effective prompts combine both:**

#### **@workspace (Scope) /explain (Action) "How does the payment controller work?"**

#### 

#### **Works cited:** 

1. About individual GitHub Copilot plans and benefits, accessed on February 1, 2026, [https://docs.github.com/en/copilot/concepts/billing/individual-plans](https://docs.github.com/en/copilot/concepts/billing/individual-plans)  
2. GitHub Copilot · Plans & pricing, accessed on February 1, 2026, [https://github.com/features/copilot/plans](https://github.com/features/copilot/plans)  
3. GitHub Copilot Data Pipeline Security, accessed on February 1, 2026, [https://resources.github.com/learn/pathways/copilot/essentials/how-github-copilot-handles-data/](https://resources.github.com/learn/pathways/copilot/essentials/how-github-copilot-handles-data/)  
4. Copilot Enterprise is now generally available · community · Discussion \#110324 \- GitHub, accessed on February 1, 2026, [https://github.com/orgs/community/discussions/110324](https://github.com/orgs/community/discussions/110324)  
5. Adding repository custom instructions for GitHub Copilot, accessed on February 1, 2026, [https://docs.github.com/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot](https://docs.github.com/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot)  
6. GitHub Server Knowledge Microsoft 365 Copilot connector overview, accessed on February 1, 2026, [https://learn.microsoft.com/en-us/microsoftsearch/github-server-knowledge-overview](https://learn.microsoft.com/en-us/microsoftsearch/github-server-knowledge-overview)  
7. Responsible use of GitHub Copilot pull request summaries, accessed on February 1, 2026, [https://docs.github.com/en/copilot/responsible-use/pull-request-summaries](https://docs.github.com/en/copilot/responsible-use/pull-request-summaries)  
8. Indexing repositories for GitHub Copilot Chat, accessed on February 1, 2026, [https://docs.github.com/copilot/concepts/indexing-repositories-for-copilot-chat](https://docs.github.com/copilot/concepts/indexing-repositories-for-copilot-chat)  
9. Managing GitHub Copilot policies as an individual subscriber, accessed on February 1, 2026, [https://docs.github.com/copilot/how-tos/manage-your-account/managing-copilot-policies-as-an-individual-subscriber](https://docs.github.com/copilot/how-tos/manage-your-account/managing-copilot-policies-as-an-individual-subscriber)  
10. Overcoming Content Filtering in GitHub Copilot: Tips for Better Prompts · community · Discussion \#159805, accessed on February 1, 2026, [https://github.com/orgs/community/discussions/159805](https://github.com/orgs/community/discussions/159805)  
11. Choosing your enterprise's plan for GitHub Copilot, accessed on February 1, 2026, [https://docs.github.com/copilot/get-started/choosing-your-enterprises-plan-for-github-copilot](https://docs.github.com/copilot/get-started/choosing-your-enterprises-plan-for-github-copilot)