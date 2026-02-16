### **GH-300 Exam Cheat Sheet: Domain 6 (Testing with GitHub Copilot)**

**Exam Weight:** 9%

**Focus:** Generating Unit Tests, Slash Commands (/tests, /setupTests), and discovering Edge Cases.

#### **1\. The Slash Commands for Testing (Memorize This)**

These are the primary tools you will use.

| Command | Action | Exam Scenario |
| :---- | :---- | :---- |
| **/tests** | **Generate unit tests** for the selected code. | "You have a calculateTax function. How do you quickly create a test suite for it?" \-\> Select code \-\> /tests. |
| **/setupTests** | **Configure a testing framework.** | "You are starting a new Python project and don't have pytest configured yet. How can Copilot help?" \-\> /setupTests (suggests frameworks and setup steps). |
| **/fixTestFailure** | **Fix a failing test.** | "Your test failed in the CI pipeline or local runner. How do you resolve it?" \-\> Use /fixTestFailure (or click the sparkle icon in Test Explorer). |

#### 

#### **2\. Generating Tests: The 3-Step Strategy**

The exam will ask how to improve the *quality* of generated tests.

1. **Select & Ask:** Highlight the function you want to test. (Copilot needs context\!).  
2. **Refine (The "Edge Case" Rule):**  
   * *Standard Prompt:* "Generate unit tests for this." (Returns basic happy-path tests).  
   * *Exam-Grade Prompt:* "Generate unit tests for this, **including edge cases for null inputs and negative numbers**."  
   * **Key Lesson:** Copilot is good at the "Happy Path" (working code). You must explicitly ask it to test the "Sad Path" (errors/exceptions).  
3. **Context Matters:**  
   * If you already have an existing test file (e.g., existing\_tests.js), **open it** in a tab. Copilot will match the style of your new tests to the existing ones (Few-Shot Learning).

#### **3\. Test Types (Vocabulary Check)**

* **Unit Tests:** Testing a single function in isolation. (Copilot's specialty).  
* **Integration Tests:** Testing how two parts work together (e.g., API \+ Database).  
  * *Strategy:* Open both the API file and the Database file so Copilot sees both contexts.  
* **End-to-End (E2E):** Testing the full flow.  
  * *Strategy:* Copilot can write Cypress/Playwright scripts if you describe the user steps: "Write a Cypress test where a user logs in and clicks 'Buy'."

#### **4\. Quick-Fire Scenario Solver**

| Scenario | Diagnosis | Correct Action |
| :---- | :---- | :---- |
| **"I don't have a test file yet."** | **Scaffolding needed.** | Use /tests \-\> Copilot will offer to create a *new* file for you. |
| **"Copilot wrote a test using Mocha but I use Jest."** | **Context missing.** | Add to prompt: "Use Jest syntax" OR use /setupTests to define the default framework. |
| **"The generated test fails immediately."** | **Hallucination or Logic Error.** | Do **not** just run it again. Read the test logic. Use /fix on the failing test to ask Copilot to correct it. |
| **"How do I find gaps in my testing?"** | **Coverage analysis.** | Ask: "What edge cases are missing from this test suite?" |

