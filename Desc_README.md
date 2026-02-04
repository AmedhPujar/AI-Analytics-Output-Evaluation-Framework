# AI Analytics Output Evaluation Framework  
### Human-in-the-Loop Validation of AI-Generated Data Insights

## Project Overview

This project demonstrates a **human-in-the-loop framework for evaluating AI-generated analytical insights**.  
Instead of building predictive models, the focus is on **assessing the correctness, safety, and reasoning quality of AI outputs** produced from partial data context — a common real-world scenario in analytical AI systems.

The project mirrors how modern analytics copilots and AI reporting tools are reviewed by human analysts before insights are trusted or surfaced to end users.

---

## Objective

To evaluate whether AI-generated data insights:
- Use **appropriate statistical reasoning**
- Avoid **overgeneralization and misleading conclusions**
- Handle **uncertainty, variance, and skew** correctly
- Produce **business-safe interpretations**

The goal is **not to test AI accuracy**, but to test **human judgment in identifying and correcting flawed AI reasoning**.

---

## Role of AI in This Project

- AI acts as a **junior analyst** that generates interpretations based on:
  - Dataset schema
  - Summary statistics
  - Small representative samples
- AI outputs are **intentionally unconstrained**, allowing reasoning errors to surface
- The human evaluator (me) reviews, validates, and corrects these outputs

This reflects real **human-in-the-loop AI workflows**, where AI assists analysis but humans ensure correctness and safety.

---

## Dataset Description

**Vehicle Sales & Market Trends Dataset**

Key columns used:
- `year` – vehicle manufacturing year  
- `make`, `model` – vehicle brand and model  
- `state` – state of sale  
- `condition` – vehicle condition score  
- `odometer` – mileage  
- `mmr` – market reference value  
- `selling_price` – final transaction price  
- `sale_date` – date of sale  

The dataset contains **tens of thousands of transactions**, enabling analysis of pricing behavior, market benchmarks, and variance.

---

## Human Baseline Analysis (Ground Truth)

Before evaluating AI outputs, a **human baseline analysis** was performed using Python (Pandas, NumPy, Seaborn).

### Key validated insights:
- Selling price deviations from MMR are **highly skewed**
- **Median** is more representative than mean due to long tails
- Mileage–price relationship is **non-linear and heteroscedastic**
- Mileage impact varies significantly by **vehicle age**
- Vehicle condition improves median outcomes but shows **large overlap**
- State-level price comparisons require **volume and MMR normalization**

These findings serve as the **ground truth** against which AI reasoning is evaluated.

---

## AI Output Generation

AI outputs were generated using a large language model (LLM) based on:
- Dataset schema
- Contextual descriptions
- High-level prompts (no corrective guidance)

### Prompts included:
1. General pricing trends
2. Mileage impact on pricing
3. Condition impact on pricing
4. State-level price comparison
5. Selling price vs market benchmark (MMR)

AI responses were captured **verbatim** for evaluation.

---

## AI Output Evaluation Framework

Each AI response was evaluated across the following dimensions:

- **Statistical correctness**
- **Metric selection (mean vs median, normalization)**
- **Reasoning quality**
- **Handling of variance and uncertainty**
- **Risk of misleading interpretation**

### Rating System
- ✅ Correct  
- ⚠️ Partially Correct / Overstated  
- ❌ Incorrect / Misleading  

---

## Evaluation Summary

### Common AI Reasoning Errors Identified:
- Overgeneralization from correlations
- Linear assumptions on non-linear relationships
- Mean-based conclusions on skewed distributions
- Ignoring variance and overlap
- Unsafe geographic comparisons without normalization
- Overconfidence under partial context

### Example Correction:
> AI Claim: “Mileage strongly determines selling price.”  
>  
> Human Evaluation:  
> The relationship is non-linear and conditional on vehicle age, with high variance at low mileage levels. Mileage alone is insufficient for strong pricing conclusions.

---

## AI Reasoning Quality Scorecard

| Dimension | Assessment |
|--------|-----------|
| Directional accuracy | Mostly correct |
| Statistical rigor | Weak |
| Handling of variance | Poor |
| Metric robustness | Inconsistent |
| Safety of conclusions | Risky |
| Human correction required | High |

---

## Key Takeaway

This project demonstrates that:
- AI can generate **plausible but unsafe analytical narratives**
- Human analysts are essential to:
  - Validate reasoning
  - Detect statistical fallacies
  - Prevent misleading insights
- Effective AI systems require **human judgment, not blind automation**

---

## Tools & Technologies

- Python  
- Pandas, NumPy  
- Seaborn, Matplotlib  
- Jupyter Notebook  
- Large Language Model (Gemini / GPT) for output generation  

---

## Project Structure

