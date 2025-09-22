# mama health - Data Scientist Challenge 🧑‍⚕️

Welcome, and thank you for your interest in joining mama health! This challenge is designed to simulate a real-world task you would encounter as part of our team. It will test your ability to handle unstructured and incomplete data, leverage modern AI tools, structure a problem, and derive business-oriented insights.

We respect your time and have designed this exercise to be completed in **4-6 hours**. Please don't feel the need to build a perfect, production-ready system. We're most interested in your approach, your assumptions, and how you translate data into a compelling story and how you find solutions **out of the box**. 

Good luck! ✨

---

## The Business Context 🎯

A major pharmaceutical company, "PharmaCorp," is preparing to launch a new biologic treatment for **Crohn's Disease**, a chronic inflammatory bowel disease. Biologics are powerful, genetically engineered drugs that represent a significant step up in treatment, but they are also expensive and can have notable side effects.

PharmaCorp's commercial team needs to understand the current treatment landscape to position their new drug effectively. They don't just want to know *what* treatments patients are on; they want to understand the *why*. Their key audience is patients with moderate-to-severe Crohn's who are **not yet on a biologic**.

Our platform gathers these patient stories longitudinally, but not all stories are complete. Some patients disengage from providing their story over time (i.e., they **churn**), leaving us with partial journey data. This is a critical real-world challenge, as these incomplete narratives could hide important insights.

**PharmaCorp's core questions are:**

1. What percentage of patients in our dataset appear to be on a biologic treatment?
2. For patients *not* on a biologic, what are the primary reasons? Is it due to doctor's recommendations, patient fears (e.g., needles, side effects), cost, or something else?
3. What other treatments are commonly discussed or tried before a biologic is considered?
4. What does a typical referral pathway look like? How many steps does it take for a patient to get from their General Practitioner (GP) to a specialist who can prescribe a biologic?

---

## Your Mission 🚀

Your mission is to analyze a dataset of 50 synthetic patient interview transcripts. Using a Large Language Model (LLM), you will extract structured information from this raw text to answer PharmaCorp's key business questions and present your findings, paying special attention to the limitations imposed by incomplete data.

---

## The Dataset 📁

In the `/data` directory, you'll find `interviews.json`. This file contains a list of 50 JSON objects, each with a `patient_id` and an `interview_transcript`.

The transcripts are intentionally messy to mimic real-world data. They will vary in length and completeness. Some patients will tell their story clearly, while others might be vague or omit key details. **The incompleteness of some transcripts can be attributed to patient churn.**

**Example Snippet 1 (Relatively Complete):**

`"It started with stomach pain, so I went to my family doctor. He thought it was just IBS. After six months of getting nowhere, I finally got a referral to a gastroenterologist, Dr. Evans. She did a colonoscopy and diagnosed me with Crohn's. We started with mesalamine, but it didn't help much. Then we tried azathioprine, but I had a bad reaction. Finally, she suggested Humira, which is a biologic. I was scared of the injections at first, but it's been a lifesaver."`

**Example Snippet 2 (Incomplete, possible churn):**

`"Yeah, the diagnosis took forever. Saw a few doctors. One gave me some pills, I forget the name. Didn't do much. The specialist mentioned a stronger medicine, an injection I think, but my insurance was a pain... anyway, that's all I remember for now."`

---

## Core Tasks ✅

### 1. Setup

- Clone this repository.
- Create a virtual environment and install the dependencies from `requirements.txt`.
- Generate a free Gemini API key from **Google AI Studio**: https://aistudio.google.com/apikey
- Create a `.env` file

### 2. Data Extraction & Structuring (The LLM part)

This is the central part of the challenge. Your goal is to use an LLM to transform the unstructured text from `interviews.json` into a structured format.

- **Use `litellm`** to interact with the Gemini API. This library provides a unified interface for calling different LLM providers. [LiteLLM Gemini Docs](https://docs.litellm.ai/docs/providers/gemini)
- **Define a data schema using Pydantic.** Create a Pydantic model (or models) to hold the extracted information for each patient (including socio-demographic data). This forces you to think about the ideal structured output.
- **Write a script** that iterates through the patient interviews, uses the LLM to extract the information, and populates your Pydantic models. **Handling uncertainty is key.**

### 3. Analysis & Insight Generation

Once you have your structured data (e.g., a list of Pydantic objects or a pandas DataFrame), analyze it to answer PharmaCorp's business questions.

- Perform the necessary calculations (e.g., percentages, counts).
- Synthesize your findings. Go beyond just the numbers. What is the *story* the data tells? What are the main barriers to biologic adoption?
- **Address Data Limitations:** This is crucial. Specifically comment on the incomplete journeys. **How might patient churn introduce bias into your analysis?** For example, are patient not going to the doctor or it's just because they churn (during the interview process) and not answer the question? How would you communicate this uncertainty and the limitations of your findings to the PharmaCorp stakeholders? How would you consider in your analysis. 

### 4. Code Quality

- **Typing:** Use Python's type hints throughout your code.
- **Unit Tests:** Write at least **two simple unit tests** using a framework like `pytest`. These could test a data cleaning function or a part of your extraction logic. We want to see that you think about code reliability.

---

## What We're Looking For 🌟

- **Problem Structuring:** How you translate the business problem into a data extraction and analysis plan. Your choice of Pydantic schema is a big part of this.
- **Technical Execution:** Your ability to write clean, well-documented Python code and correctly use tools like `litellm`, Pydantic, and `pytest`.
- **Handling Ambiguity:** How you deal with incomplete or contradictory information. We're especially interested in how you reason about the impact of churn on the validity of your insights. Document your assumptions clearly.
- **Business Acumen:** The quality and clarity of your final insights. Can you present your findings in a way that is directly useful to a commercial team, including the necessary caveats?

---

Here's an improved version:

## Deliverables 📦

Please submit a link to your forked and completed GitHub repository. **Keep the repository private** and send an invite to **lorenzo.famiglini@mamahealth.com**.

The repository should contain:

1. **`src/`** directory - All your source code

2. **`tests/`** directory - Your unit tests

3. **`requirements.txt`** - All dependencies with pinned versions

4. **`README.md`** - Updated with your final analysis, including:
   - **Business Questions**: Present your answers to all four questions, supported by data and visualizations
   - **Data Limitations**: Discuss the limitations of the data (particularly regarding churn)
   - **Methodology**: Explain your approach, assumptions, and any challenges you faced
     
---

## Optional "Go the Extra Mile" Tasks 🚀

Have extra time? Want to impress us further? Consider one of the following (these are **completely optional**):

- **Error Handling & Validation:** Implement more robust error handling for the LLM calls (e.g., retries). Use Pydantic's validation capabilities to clean or standardize the LLM's output.
- **Advanced Visualization:** Create a compelling chart or diagram to visualize the patient journey or the referral pathway (e.g., a Sankey diagram).
- **Develop a Small Chain-of-Thought Prompt:** Instead of a single large prompt, experiment with a multi-step prompt to first identify key sentences and then extract entities from those sentences.
- **Containerize It:** Include a `Dockerfile` to containerize your analysis script.
- **Usage of OS models** (from one shot classification, till topic modelling): [HuggingFace](https://huggingface.co/)
