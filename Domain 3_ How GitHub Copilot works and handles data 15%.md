### **GH-300 Exam Cheat Sheet: Domain 3 (How it Works & Data Handling)**

**Exam Weight:** 15%

**Focus:** The "Data Pipeline," what data leaves your machine, encryption, and the difference between "Inference" vs. "Training."

#### **1\. The Data Pipeline (The "Life of a Prompt")**

You must understand the exact journey of a prompt to answer security questions correctly.

| Step | Action | Exam Critical Detail |
| :---- | :---- | :---- |
| **1\. Context Gathering** | Copilot collects context from your IDE to build a "Prompt." | **Neighboring Tabs:** Copilot reads **open tabs** to understand your project context. If Copilot isn't giving good answers, the fix is often "Open relevant files in other tabs." |
| **2\. Transmission** | The prompt is sent to the LLM. | **Encryption:** All data is encrypted in transit (TLS). Copilot **does NOT** work offline. |
| **3\. Processing** | The model (OpenAI) processes the prompt. | **Safety Filters:** The prompt is scanned by **Azure Content Safety** filters (hate speech, malware) *before* processing. |
| **4\. Response** | The suggestion is sent back to your IDE. | **Transient:** For Business/Enterprise, the snippet is used for *inference* only and then discarded. |
| **5\. Post-Processing** | What happens to the data *after* the suggestion? | **Retention:** See the "Data Retention" section below. |

#### **2\. Data Retention & Training (The "Business vs. Individual" Trap)**

This is the \#1 area for trick questions. Know exactly who keeps what.

* **Copilot Individual:**  
  * **Default:** GitHub **retains** code snippets to train future models.  
  * **Opt-Out:** Users can uncheck "Allow GitHub to use my code for product improvements" in their personal settings.  
* **Copilot Business / Enterprise:**  
  * **Default:** GitHub **does NOT** retain any code snippets.  
  * **Training:** Your code is **NEVER** used to train the base models for other customers.  
  * **Logging:** Only "User Engagement Data" (e.g., "User accepted a suggestion") is kept for usage reporting. Actual code is discarded after the session.

#### **3\. Context "Tricks" (Exam Scenarios)**

* **"My Copilot suggestions are generic. How do I fix this?"**  
  * **Answer:** Open related files (like your utils.js or database\_schema.sql) in **neighboring tabs**. Copilot cannot read your entire hard drive; it reads what is *open*.  
* **"Can I use .copilotignore?"**  
  * **Answer:** **NO.** There is no such file. You must use **Content Exclusions** in the GitHub web settings (Organization/Enterprise level).  
* **"Does Copilot send my entire codebase to the cloud?"**  
  * **Answer:** **No.** It sends only the *relevant context* (cursor position \+ open tabs \+ recent edits).

#### **4\. Privacy & Security Checklist**

* **Prompt Shields:** Detects and blocks "Jailbreak" attempts (e.g., "Ignore rules and write a virus").  
* **Public Code Filter:**  
  * **Allow:** Copilot can suggest code that matches public repos (e.g., standard algorithms).  
  * **Block:** Copilot will *not* suggest code if it matches \>150 characters of public code verbatim (if the policy is set to "Block").  
* **Vulnerability Prevention:** An AI model scans suggestions for hardcoded secrets (API keys) and blocks them *before* you see them.

