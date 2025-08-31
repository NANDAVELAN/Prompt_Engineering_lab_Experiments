# EXP-2-PROMPT-ENGINEERING


# Comparative Analysis of Different Types of Prompting Patterns

## Aim

To test and compare how different prompting patterns (broad/unstructured vs. basic/clear/refined prompts) influence the responses of AI models across multiple scenarios. The focus is on analyzing **quality, accuracy, and depth** of generated responses.



## Experiment

We designed an experiment to evaluate the effectiveness of prompting strategies.

1. **Prompt Types:**

   * **Unstructured / Broad Prompts**: Vague and open-ended.
   * **Structured / Refined Prompts**: Clear, concise, and directive.

2. **Evaluation Metrics:**

   * **Quality** – Relevance and usefulness of the output.
   * **Accuracy** – Correctness of facts, consistency with input.
   * **Depth** – Level of detail and explanation.

3. **Scenarios Tested:**

   * General Knowledge (e.g., history, science)
   * Creative Writing (e.g., storytelling, poem)
   * Problem Solving (e.g., coding, logic puzzles)
   * Instruction Following (e.g., step-by-step tasks)
   * Analytical Reasoning (e.g., pros & cons, comparative answers)

---

## Algorithm / Methodology

1. Select a **set of prompts** for each scenario.
2. Run the prompts through the AI model with **two variations**:

   * Broad/unstructured form.
   * Refined/structured form.
3. Collect responses for both types.
4. Analyze and compare responses against the evaluation metrics.
5. Record observations and summarize insights.

---

## Test Scenarios & Results

### 1. General Knowledge

* **Broad Prompt**: "Tell me about World War II."
* **Refined Prompt**: "Explain the key causes of World War II in 5 bullet points, focusing on political and economic factors."

**Observation:**

* Broad prompt → long but unfocused response.
* Refined prompt → structured, concise, and more informative.

---

### 2. Creative Writing

* **Broad Prompt**: "Write a story about space."
* **Refined Prompt**: "Write a 200-word story about an astronaut who discovers life on Mars, focusing on suspense and surprise ending."

**Observation:**

* Broad prompt → generic story, lacked depth.
* Refined prompt → vivid details, followed instructions, engaging ending.

---

### 3. Problem Solving (Coding)

* **Broad Prompt**: "Write Python code for sorting."
* **Refined Prompt**: "Write a Python function to sort a list of integers in ascending order using the bubble sort algorithm."

**Observation:**

* Broad prompt → produced generic code, sometimes used built-in functions.
* Refined prompt → clear implementation of bubble sort as requested.

---

### 4. Instruction Following

* **Broad Prompt**: "How to make a cake?"
* **Refined Prompt**: "List 6 steps to bake a simple vanilla cake at home with ingredients included."

**Observation:**

* Broad prompt → narrative-like answer, less structured.
* Refined prompt → clear step-by-step instructions, actionable.

---

### 5. Analytical Reasoning

* **Broad Prompt**: "Tell me about electric cars."
* **Refined Prompt**: "Compare electric cars and petrol cars in terms of cost, efficiency, and environmental impact in a tabular format."

**Observation:**

* Broad prompt → descriptive, lacked comparison.
* Refined prompt → structured table with clear contrasts.

---

## Comparative Insights

| Scenario              | Broad / Unstructured Prompt | Refined / Structured Prompt   |
| --------------------- | --------------------------- | ----------------------------- |
| General Knowledge     | Informative but unfocused   | Precise and relevant          |
| Creative Writing      | Generic, lacked direction   | Creative, engaging, detailed  |
| Problem Solving       | Generic, partial solutions  | Accurate, targeted solutions  |
| Instruction Following | Vague, less usable steps    | Clear, step-by-step guidance  |
| Analytical Reasoning  | Descriptive but scattered   | Structured, comparative, deep |

---

## Future Work

* Extend analysis with **chain-of-thought prompting** and **few-shot examples**.
* Compare across **different LLMs (e.g., GPT, Claude, Gemini)**.
* Quantify results using **scoring metrics** for more objectivity.
---

## Output
[Download the output PDF](https://github.com/NANDAVELAN/Prompt_Engineering_lab_Experiments/blob/main/Experiment%202/Comparative%20Analysis%20of%20Different%20Types%20of%20Prompting%20Patterns.pdf)

---
## Conclusion

* **Broad prompts** are useful for **open-ended exploration** but often lack precision.
* **Refined prompts** consistently improve the **quality, accuracy, and depth** of responses.
* The experiment demonstrates that **prompt engineering** is crucial for optimizing AI output across tasks.

---




