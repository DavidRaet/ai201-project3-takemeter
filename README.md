# TakeMeter

> A fine-tuned text classifier for evaluating discourse quality in [COMMUNITY NAME].

***

## Project Overview

<!--
1–3 sentences describing what TakeMeter does, what community it targets,
and what problem it solves. Keep it direct.
-->

***

## Label Taxonomy

<!--
List your 2–4 labels with their definitions (same as planning.md, kept in sync).
Brief enough for a reader to understand what each label means without the full planning doc.
-->

| Label | Definition |
|-------|------------|
| [Label 1] | <!-- One-sentence definition --> |
| [Label 2] | <!-- One-sentence definition --> |
| [Label 3] | <!-- One-sentence definition (if applicable) --> |
| [Label 4] | <!-- One-sentence definition (if applicable) --> |

***

## Dataset

**Source:** <!-- Where the data came from (e.g., r/[subreddit] via Reddit API / PRAW) -->

**Size:** <!-- Total examples, e.g., 250 posts -->

**Labeling process:**
<!--
How posts were labeled. If an LLM was used for pre-labeling, disclose it here:
e.g., "Posts were pre-labeled using [model] with the prompt in /prompts/annotation_prompt.txt,
then manually reviewed and corrected."
-->

**Label distribution:**

| Label | Count | % of Dataset |
|-------|-------|--------------|
| [Label 1] | <!-- N --> | <!-- % --> |
| [Label 2] | <!-- N --> | <!-- % --> |
| [Label 3] | <!-- N --> | <!-- % --> |
| [Label 4] | <!-- N --> | <!-- % --> |
| **Total** | | **100%** |

### Difficult Examples

<!--
Describe at least 3 genuinely hard labeling cases. For each:
- Paste or paraphrase the post
- State which label you chose
- Explain why it was hard and how you resolved it
-->

**Example 1:**
> <!-- Post text -->

Label assigned: `[LABEL]`
Difficulty: <!-- Why this was ambiguous and what tipped the decision -->

***

**Example 2:**
> <!-- Post text -->

Label assigned: `[LABEL]`
Difficulty: <!-- Why this was ambiguous and what tipped the decision -->

***

**Example 3:**
> <!-- Post text -->

Label assigned: `[LABEL]`
Difficulty: <!-- Why this was ambiguous and what tipped the decision -->

***

## Fine-Tuning Pipeline

**Base model:** <!-- e.g., distilbert-base-uncased, roberta-base, etc. -->

**Training platform:** <!-- e.g., Google Colab, local GPU, HuggingFace AutoTrain -->

**Key training decision:**
<!--
Describe at least one deliberate training choice and your reasoning:
e.g., "I used 5 epochs instead of the default 3 because validation loss was still decreasing at epoch 3.
By epoch 5, it plateaued, suggesting the model had converged on the available data."
Do NOT just say "I used the default."
-->

***

## Baseline Comparison

**Baseline approach:**
<!--
Describe the zero-shot or few-shot LLM baseline:
- What model was used
- The exact prompt (or reference to /prompts/baseline_prompt.txt)
- How results were collected (manual inference? API calls? how many examples evaluated?)
-->

**Prompt used:**
```
[Paste your baseline classification prompt here]
```

**Performance comparison:**

| Metric | Fine-Tuned Model | Baseline |
|--------|-----------------|----------|
| Overall Accuracy | <!-- --> | <!-- --> |
| Macro F1 | <!-- --> | <!-- --> |
| [Label 1] F1 | <!-- --> | <!-- --> |
| [Label 2] F1 | <!-- --> | <!-- --> |
| [Label 3] F1 | <!-- --> | <!-- --> |

***

## Evaluation Report

### Per-Class Metrics

<!-- Report at least one per-class metric (precision, recall, or F1) for the fine-tuned model. -->

| Label | Precision | Recall | F1 |
|-------|-----------|--------|----|
| [Label 1] | <!-- --> | <!-- --> | <!-- --> |
| [Label 2] | <!-- --> | <!-- --> | <!-- --> |
| [Label 3] | <!-- --> | <!-- --> | <!-- --> |
| **Macro Avg** | <!-- --> | <!-- --> | <!-- --> |

### Confusion Matrix

<!--
Paste a confusion matrix table or image here. Rows = actual labels, Columns = predicted labels.
-->

| Actual \ Predicted | [Label 1] | [Label 2] | [Label 3] |
|--------------------|-----------|-----------|-----------|
| **[Label 1]** | <!-- --> | <!-- --> | <!-- --> |
| **[Label 2]** | <!-- --> | <!-- --> | <!-- --> |
| **[Label 3]** | <!-- --> | <!-- --> | <!-- --> |

### Wrong Prediction Analysis

<!--
Analyze at least 3 specific incorrect predictions. For each:
- The post text
- The true label vs predicted label
- An explanation tied to the data, the label boundary, or the model's behavior
NOT just "it got it wrong."
-->

**Misclassification 1:**
> <!-- Post text -->

True label: `[LABEL]` → Predicted: `[LABEL]`
Analysis: <!-- What specifically caused this error — data issue, boundary ambiguity, or model behavior? -->

***

**Misclassification 2:**
> <!-- Post text -->

True label: `[LABEL]` → Predicted: `[LABEL]`
Analysis: <!-- ... -->

***

**Misclassification 3:**
> <!-- Post text -->

True label: `[LABEL]` → Predicted: `[LABEL]`
Analysis: <!-- ... -->

***

### Failure Pattern Reflection

<!--
This is the 2-point section. Do NOT write "it needs more data."
Identify a specific failure pattern:
- A label pair the model consistently confuses and WHY
- A type of post that systematically breaks the model
- A distributional issue (e.g., training examples for Label X were all from one context, but test set had broader variety)

Connect the observed confusion matrix and error examples to a root cause in your data or label design.
-->

***

## AI Usage and Spec Reflection

### AI Tool Usage

<!--
Describe at least 2 specific instances of AI tool use. For each instance:
1. What you directed the AI to do
2. What the AI produced
3. What you revised, overrode, or corrected

If an LLM assisted with annotation, disclose: which model, what prompt, and how you verified outputs.
-->

**Instance 1:**
- Directed: <!-- What task you gave the AI -->
- Output: <!-- What it produced -->
- Override/revision: <!-- What you changed and why -->

**Instance 2:**
- Directed: <!-- ... -->
- Output: <!-- ... -->
- Override/revision: <!-- ... -->

### Spec Reflection

<!--
Two things required:
1. One way the spec (planning.md) helped guide the actual work
2. One way the implementation diverged from the spec and why

Be substantive — not "the spec helped me stay organized."
-->

**Where the spec guided the work:**
<!-- ... -->

**Where implementation diverged:**
<!-- ... -->

***

## Repository Structure

```
takemeter/
├── data/
│   ├── raw/             # Raw scraped posts
│   └── annotated/       # Labeled dataset (CSV or JSONL)
├── prompts/
│   ├── baseline_prompt.txt
│   └── annotation_prompt.txt   # (if LLM-assisted)
├── notebooks/
│   └── finetune.ipynb
├── results/
│   └── eval_report.json
├── planning.md
└── README.md
```

***

## Setup

```bash
# Clone
git clone https://github.com/[your-username]/ai201-project3-takemeter.git
cd ai201-project3-takemeter

# Install dependencies
pip install -r requirements.txt
```

<!-- Add any other setup steps specific to your training platform -->
