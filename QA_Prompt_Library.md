# QA Prompt Library (Automation Focus)

> Tested with ChatGPT‑4o and Claude 3.5. Optimize by adding **project context** (domain, stack, user roles).

---

## 1) Test Design (Cypress, POM)
**Intent:** Generate maintainable Cypress tests using the Page Object Model.  
**Prompt:**
```
Act as a senior QA automation engineer. Based on the acceptance criteria below, generate Cypress tests using the Page Object Model. 
Requirements:
- Positive + negative scenarios
- before/after hooks
- data‑cy selectors
- assertions for URL, UI, and API (use cy.intercept where relevant)
Output: code blocks with file paths and brief comments.
Acceptance criteria:
<PASTE HERE>
```
**Example Input:** Login with email/password; invalid creds show error.

---

## 2) Flaky Test Diagnosis
**Intent:** Identify root causes and stabilise tests.  
**Prompt:**
```
You are a QA lead diagnosing flaky Cypress tests. Here is a failing test log and spec. 
Tasks:
- Identify likely root causes (timing, async, network, selectors)
- Suggest concrete fixes (cy.intercept, explicit waits, retries, test isolation)
- Propose if the test should be rewritten, skipped, or stabilised
Provide a concise checklist of changes.
Log/spec:
<PASTE HERE>
```

---

## 3) Refactor for Readability/DRY
**Intent:** Improve maintainability and conventions.  
**Prompt:**
```
Review the following Cypress spec and refactor it for readability and DRY. 
Enforce consistent naming, extract page objects, and replace brittle selectors with data‑cy.
Return a diff‑style suggestion and the final code.
Spec:
<PASTE HERE>
```

---

## 4) Synthetic Test Data (API)
**Intent:** Create edge‑case rich datasets.  
**Prompt:**
```
Generate a JSON dataset with 10 valid and 10 invalid user objects for registration testing.
Include boundary values, unicode, special characters, and missing fields.
Return as a single JSON array.
```

---

## 5) Traceability → Automation Plan
**Intent:** Map manual tests to automation backlog.  
**Prompt:**
```
Given this list of manual test cases, identify which are automatable.
Prioritise by risk, frequency, and data complexity. 
Return a table: Case ID | Automatable (Y/N) | Rationale | Priority | Suggested framework
Manual test list:
<PASTE HERE>
```

---

## 6) Regression Analysis (Last 3 Runs)
**Intent:** Stabilise the suite efficiently.  
**Prompt:**
```
Analyse the failed tests across the last 3 regression runs.
Group by root cause, estimate fix effort, and propose ROI‑based order of fixes.
Return:
- Grouped causes
- Top 5 fixes with rationale
- Quick wins for CI stability
Data:
<PASTE HERE>
```

---

## 7) Bug Pattern Mining
**Intent:** Link defects to weak coverage.  
**Prompt:**
```
Summarise patterns across these bug reports. Map each pattern to test coverage gaps and propose targeted exploratory charters.
Bugs:
<PASTE HERE>
```

---

## 8) Code Generation: Forgot Password
**Intent:** Produce robust e2e with network assertions.  
**Prompt:**
```
Generate Cypress tests for the 'Forgot Password' flow.
Use cy.intercept to assert API requests/responses and handle both success and failure notifications.
Return file‑scoped code blocks.
```

---

## 9) Prompt Self‑Evaluation
**Intent:** Improve test quality automatically.  
**Prompt:**
```
Evaluate the following test cases for completeness, naming consistency, and duplication. 
Rate each 1–5 for coverage and readability, and propose one improvement per case.
Test cases:
<PASTE HERE>
```

---

## 10) Automation Report Draft
**Intent:** Convert runs into stakeholder‑friendly reports.  
**Prompt:**
```
Convert this test run summary into a QA report with exec‑level highlights: coverage, pass/fail, flakiest modules, and blockers. 
Keep under 250 words and include next‑step recommendations.
Run summary:
<PASTE HERE>
```

---

### Tips
- Add **role**, **domain**, and **constraints** to every prompt.
- Iterate: **Generate → Review → Refine → Apply**.
- Save your best prompts per project in version control.
