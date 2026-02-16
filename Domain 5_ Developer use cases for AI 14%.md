### **GH-300 Exam Cheat Sheet: Domain 5 (Developer Use Cases)**

**Exam Weight:** 14%

**Focus:** Refactoring, Debugging, Slash Commands (/fix, /doc), and generating Unit Tests.

#### **1\. The "Slash Commands" (Memorize These)**

You will likely get questions asking "Which command should the developer use?"

| Command | Function | Exam Scenario |
| :---- | :---- | :---- |
| **/fix** | **Propose a fix for problems in code.** | "A developer sees a red squiggly line (lint error) or a compile error. What is the fastest way to resolve it?" \-\> Highlight code \-\> /fix. |
| **/doc** | **Generate documentation.** | "You need to add JSDoc comments to a legacy function before checking it in." \-\> /doc. |
| **/tests** | **Generate unit tests.** | "You have written a function but no tests. How do you quickly create a test suite?" \-\> /tests. |
| **/explain** | **Explain how code works.** | "A new developer joins the team and doesn't understand a complex RegEx pattern." \-\> /explain. |
| **/optimize** | **Improve performance/readability.** | "The code works but is slow or hard to read." \-\> /optimize. |
| **@workspace** | **Ask about the whole project.** | "Where is the Login class defined?" or "How is authentication handled in this app?" \-\> @workspace. |

#### 

#### **2\. Refactoring & Debugging Strategies**

* **Refactoring:**  
  * **Scenario:** You have a long, messy function.  
  * **Action:** Highlight the code and type: *"Refactor this to be more modular"* or *"Split this into smaller functions."*  
  * **Key Concept:** Copilot does not *change* your code automatically. It **suggests** a change, and you must "Accept" or "Apply" it.  
* **Debugging:**  
  * **Scenario:** You have a runtime error in the terminal.  
  * **Action:** Copy the stack trace (error message) from the terminal \-\> Paste it into Copilot Chat \-\> Ask "Fix this."  
  * **Note:** Copilot is great at reading stack traces.

#### **3\. Generating Unit Tests (The "Rule of 3")**

When generating tests, the exam expects you to know *what* to ask for.

1. **Positive Cases:** "Test that the function returns X when given Y." (The Happy Path).  
2. **Negative Cases:** "Test that it throws an error when input is null." (Edge Cases).  
3. **Framework:** "Use Jest syntax" or "Use PyTest." (Be specific).

#### **4\. Quick-Fire Scenario Solver**

| Scenario | Diagnosis | Correct Action |
| :---- | :---- | :---- |
| **"I need to understand a SQL query."** | **Explanation needed.** | Highlight query \-\> /explain. |
| **"I want to find a security bug."** | **Vulnerability scan.** | Ask: "Does this code have any security vulnerabilities?" (Copilot is not a dedicated security tool, but can find common issues like SQLi). |
| **"I want to translate code from Python to Go."** | **Translation.** | Highlight Python code \-\> Ask "Translate this to Go." |
| **"Copilot is suggesting code for a library I don't use."** | **Context issue.** | You didn't specify the framework. Add context: "Using React..." |

