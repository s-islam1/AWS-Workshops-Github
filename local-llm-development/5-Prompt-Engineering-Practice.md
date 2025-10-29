
### 🧩 `1-introduction.md`

# Prompt Engineering - Introduction

Welcome to the **Prompt Engineering Lab**!

In this lab, you will learn how to design and optimize prompts to guide Large Language Models (LLMs) such as ChatGPT or local models like Mistral, Gemma, or Llama running on your system.

---

## 🎯 Learning Objectives

By the end of this lab, you will be able to:

- Define prompt engineering and explain why it’s considered *engineering*.
- Differentiate between zero-shot, few-shot, and chain-of-thought prompting.
- Demonstrate how changing a prompt changes the model’s behavior and tone.

---

## 🧠 What is Prompt Engineering?

**Prompt Engineering** is the process of *designing*, *testing*, and *refining* instructions that lead an AI model to produce a desired output.

It’s called “engineering” because you are:
- **Designing** logical systems using language instead of code.
- **Testing** prompts for reliability, clarity, and consistency.
- **Iterating** to optimize model performance and reduce ambiguity.

Prompt engineers are like **UX designers for AI models** — crafting interfaces between human intent and machine intelligence.

---

## ⚙️ Basic Prompt Types

| Type | Description | Example |
|------|--------------|----------|
| **Zero-shot** | Ask directly, no examples. | “Explain cloud computing.” |
| **Few-shot** | Include examples or format instructions. | “Example: Q: What is AI? A: Artificial Intelligence is... Now explain Cloud Computing in the same format.” |
| **Chain-of-thought (CoT)** | Ask the model to reason step-by-step. | “Let’s reason step-by-step: how does a VPC isolate network traffic?” |
| **Role prompting** | Assign a role or context to control tone or depth. | “You are an AWS instructor teaching beginners about IAM.” |

---

## 🧩 Activity 1: Warm-Up

Try each of these prompt types in ChatGPT (or your local model):

1. **Zero-shot:**  
   > Explain Cloud Computing.

2. **Few-shot:**  
   > Example:  
   > Q: What is AI?  
   > A: Artificial Intelligence is the ability of computers to learn and make decisions.  
   >  
   > Now, answer in the same format:  
   > Q: What is Cloud Computing?

3. **Chain-of-thought:**  
   > Explain Cloud Computing step-by-step using a real-world analogy.

4. **Role-based:**  
   > You are an AWS Cloud Practitioner instructor. Explain Cloud Computing in AWS terms.

---

## 🧪 Reflection

After running the prompts, compare:
- Which one gave the clearest answer?
- Which one matched your desired tone or level?
- How would you refine it further?

---
```

---

### 🧠 `2-practice.md`

```markdown
# Prompt Engineering Lab - Practice

Now that you understand the core types of prompts, let’s put your skills to practice.

---

## 🎯 Objective

You will experiment with **prompt structure**, **tone**, and **constraints** to observe how a model’s output changes.

---

## 🧩 Exercise 1: Change the Audience

Prompt:
> Explain “Virtual Private Cloud (VPC)” to a 10-year-old.

Then modify:
> Explain “Virtual Private Cloud (VPC)” to a cybersecurity professional.

Compare:
- How does the tone change?
- What examples or vocabulary shift?

---

## 🧩 Exercise 2: Add Formatting Rules

Prompt:
> Summarize how IAM works.

Now refine:
> Summarize how IAM works in **3 bullet points**, each less than **15 words**.

You’ll notice the model now follows formatting rules — a sign of *precise prompt control.*

---

## 🧩 Exercise 3: Add Constraints

Prompt:
> Explain S3 in simple terms.

Now add limits:
> Explain S3 in simple terms, **under 60 words**, and include **one analogy**.

Observe:
- How constraints help control the output length and clarity.

---

## 🧩 Exercise 4: Role Play

Prompt:
> You are an AWS Support Engineer.  
> A student says: “My EC2 instance won’t start.”  
>  
> Write a short reply explaining how to troubleshoot.

This technique makes the model simulate **real-world job roles**, useful for training or support chatbots.

---

## ✅ Reflection Questions

- How does the model interpret different audiences or roles?  
- Which prompts gave you the most control?  
- What patterns seem most effective for professional communication?

---
```

---

### 🔍 `3-evaluation.md`

```markdown
# Prompt Engineering - Evaluation and Iteration

Now it’s time to **evaluate** how effective your prompts are.

---

## 🎯 Objective

You will test multiple prompts for the same task and evaluate them based on clarity, accuracy, and tone.

---

## 🧩 Step 1: Define the Task

Task:  
> Explain what Amazon EC2 is and how it differs from Amazon S3.

---

## 🧩 Step 2: Write Three Versions

1. **Zero-shot:**  
   > Explain the difference between EC2 and S3.

2. **Few-shot:**  
   > Example:  
   > EC2 = Compute service for running servers.  
   > S3 = Storage service for saving files.  
   >  
   > Now explain EC2 and S3 in the same format with one real-world analogy.

3. **Chain-of-thought:**  
   > Let’s reason step-by-step:  
   > 1. Define EC2  
   > 2. Define S3  
   > 3. Compare them  
   > 4. Give a real-world analogy.

---

## 🧩 Step 3: Create a Scoring Table

| Prompt Type | Clarity (1-5) | Accuracy (1-5) | Tone (1-5) | Total |
|--------------|----------------|----------------|-------------|--------|
| Zero-shot |   |   |   |   |
| Few-shot |   |   |   |   |
| CoT |   |   |   |   |

Use this table to score your outputs.

---

## 🧠 Step 4: Iteration

Pick the best-performing prompt and **refine it**:
- Add role context: “You are a cloud computing instructor.”
- Add formatting: “Use bullet points and one analogy.”
- Add tone: “Keep it professional but friendly.”

Re-test and re-score your prompt.

This **iteration cycle** is the heart of *prompt engineering* — small design tweaks yield big performance improvements.

---
```

---

### ⚙️ `4-advanced.md`

````markdown
# Prompt Engineering - Advanced Techniques

Welcome to the advanced lab!  
Here, you’ll learn to design **structured prompts**, **chained prompts**, and **evaluation prompts** — just like real AI engineers.

---

## 🧩 1. Prompt Templates

You can use placeholders to make reusable prompts.

```text
Explain {topic} in {words} words for {audience}.
````

**Example:**

> Explain CloudFormation in 80 words for AWS beginners.

This approach is used in frameworks like **LangChain** or **Amazon Bedrock Flows**, where templates help automate prompt generation.

---

## 🧩 2. Prompt Chaining

Chain multiple prompts to perform sequential reasoning.

**Example workflow:**

1. Prompt 1: Summarize the AWS Well-Architected Framework.
2. Prompt 2: From that summary, extract 5 quiz questions.
3. Prompt 3: Evaluate which question best checks understanding.

Each prompt feeds into the next — creating a *pipeline*.

---

## 🧩 3. Evaluation Prompts

Ask the model to *evaluate its own output.*

Example:

> Rate this explanation on a scale of 1–10 for clarity and accuracy.
> Suggest one improvement.

This creates a **feedback loop**, improving consistency without human intervention.

---

## 🧩 4. Meta-Prompting

Prompting the model *how to think*.

Example:

> Before answering, think like a teacher preparing students for the AWS Cloud Practitioner exam.
> Explain using the AWS console as an example.

Meta-prompts shape reasoning behavior and creativity — essential for *agentic AI design.*

---

## 🧠 Reflection and Discussion

* How do templates make prompts reusable in automation?
* How could chaining be used in building chatbots or teaching tools?
* What risks come from models evaluating themselves?

---

## 🚀 Challenge Activity

Design a **multi-step prompt** that:

1. Summarizes an AWS concept (like IAM or VPC),
2. Generates 3 quiz questions,
3. Evaluates the difficulty level.

This simulates how **Bedrock Agents** or **LangChain pipelines** use prompt engineering to create automated AI systems.

---

## 🏁 Conclusion

Prompt engineering bridges **human creativity** and **machine reasoning**.
It’s not just about phrasing — it’s about **designing intelligent communication systems.**

---
