### **GH-300 Exam Cheat Sheet: Domain 4 (Prompt Engineering)**

**Exam Weight:** 9%

**Focus:** The "4 S" Principle, Zero/One/Few-Shot prompting, and Context management.

#### **1\. The "4 S" Principles of Prompting (Memorize This)**

If an exam question asks "How do I improve this prompt?", the correct answer almost always involves one of these 4 concepts.

| Principle | Meaning | Exam Example |
| :---- | :---- | :---- |
| **Single** | **One task at a time.** | *Bad:* "Fix the bug, write a test, and refactor the class." *Good:* "Fix the bug in this function." (Then ask for tests later). |
| **Specific** | **Be explicit about goals.** | *Bad:* "Write code to parse data." *Good:* "Write a Python function using pandas to parse a CSV file and drop empty rows." |
| **Short** | **Concise but clear.** | *Bad:* A 3-paragraph story about why you need the code. *Good:* A direct instruction with context. |
| **Surround** | **Context matters.** | *Bad:* Asking a question with all files closed. *Good:* **Opening relevant files** (neighboring tabs) so Copilot can "see" the variable definitions. |

#### 

#### **2\. "Shot" Prompting Techniques (Exam Terminology)**

You must be able to identify which technique is being used in a scenario.

* **Zero-Shot Prompting:**  
  * **Definition:** Asking Copilot to do something *without* giving any examples.  
  * **Example:** "Write a unit test for this function."  
  * **Result:** innovative but potentially inconsistent.  
* **One-Shot Prompting:**  
  * **Definition:** Providing *one* example of what you want.  
  * **Example:** "Here is an example test case: \[Code Snippet\]. Now write a test for the Login function."  
  * **Result:** Better structure, follows your style.  
* **Few-Shot Prompting (The Gold Standard):**  
  * **Definition:** Providing *multiple* examples (2-3) to establish a pattern.  
  * **Example:** "Here are 3 examples of how we handle errors in this app: \[Ex1, Ex2, Ex3\]. Write an error handler for the new API."  
  * **Exam Strategy:** If a question asks **"How to ensure Copilot follows our specific team coding style?"**, the answer is **Few-Shot Prompting** (providing examples of that style).

#### **3\. Iterative Prompting Strategy**

* **Don't Accept the First Draft:** The exam expects you to treat Copilot as a **Pair Programmer**, not a magic wand.  
* **The Workflow:**  
  1. Write a specific prompt.  
  2. Review the output.  
  3. **Refine:** If the output is wrong, **do not write the code yourself**. Instead, **add a comment** or refine the prompt with more constraints.  
  4. **Accept:** Only accept when it's correct.

#### **4\. Quick-Fire Scenario Solver**

| Scenario | Diagnosis | Correct Action |
| :---- | :---- | :---- |
| **"Copilot is using an old library version."** | **Stale Context.** | Add a comment specifying the version: // use React 18 syntax or open the package.json file. |
| **"Copilot suggests generic code, not my project's style."** | **Lack of Context.** | Open related files (Neighboring Tabs) or use **Few-Shot Prompting** (paste an example). |
| **"I want to document legacy code."** | **Slash Command.** | Highlight the code and use /doc (or /explain to understand it first). |
| **"The prompt is too complex and fails."** | **Violation of "Single".** | Break the prompt into 3 smaller steps. |

