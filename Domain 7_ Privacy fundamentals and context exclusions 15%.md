### **GH-300 Exam Cheat Sheet: Domain 7 (Privacy & Exclusions)**

**Exam Weight:** 15%

**Focus:** Content Exclusions, Public Code Matching, and Troubleshooting why Copilot isn't working.

#### **1\. Content Exclusions (The "Kill Switch")**

You **must** know the rules of exclusions. Exam questions will ask "Why is Copilot not working in this file?"

| Feature | Rule | Exam Critical Detail |
| :---- | :---- | :---- |
| **Configuration** | **Web UI Only.** | You configure exclusions in **GitHub Organization/Enterprise Settings**. You CANNOT configure them in a local .gitignore or .editorconfig file. |
| **Scope** | **Repositories or Paths.** | You can exclude src/secrets/\* or repo-name. You **cannot** exclude based on file content (e.g., "files containing 'password'"). |
| **Effect** | **Total Blackout.** | If a file is excluded: 1\. Copilot will not make suggestions in it. 2\. Copilot Chat cannot read it. 3\. It is not sent as context even if open in a neighbor tab. |
| **Client vs. Server** | **Client Enforcement.** | The IDE extension fetches the policy and blocks the file *locally* before sending any data. |

#### 

#### **2\. Public Code Matching (The "IP Protection" Filter)**

This is the feature that protects you from legal issues.

* **The Setting:** "Suggestions matching public code."  
* **ALLOW:** Copilot *can* suggest code that matches public repositories (e.g., a standard sorting algorithm).  
* **BLOCK:** Copilot will **check every suggestion** against a database of public code on GitHub.  
  * If a match (\> \~150 chars) is found, the suggestion is **blocked** (never shown to you).  
* **Exam Scenario:** "Your company has a strict policy against using open-source code without attribution. What setting do you enable?" \-\> **Block suggestions matching public code.**

#### **3\. Troubleshooting (Why is Copilot silent?)**

If a question asks "A user is not getting suggestions," look for these answers in this order:

1. **File Type:** Is the file type supported? (Copilot works best on code, not binary files).  
2. **Exclusion:** Is the file in an **excluded path** in Org Settings?  
3. **Network:** Is a firewall blocking the connection to GitHub API?  
4. **VPN/Certificates:** Is a corporate proxy (Zscaler/Cisco) intercepting the SSL traffic? (Common enterprise issue).

#### **4\. Quick-Fire Scenario Solver**

| Scenario | Diagnosis | Correct Answer |
| :---- | :---- | :---- |
| **"I want to stop Copilot from reading my .env files."** | **Exclusion Needed.** | Go to Org Settings \-\> Content Exclusions \-\> Add \*\*/\*.env. |
| **"Copilot icon has a diagonal line through it."** | **Disabled/Excluded.** | The current file is likely excluded by policy. |
| **"Can I exclude files just for myself?"** | **No.** | Content exclusions are an **Organization/Enterprise** level setting, not a personal user setting. |
| **"Does Copilot use my excluded files for training?"** | **No.** | Excluded files are never sent to the server, so they cannot be used for training. |

