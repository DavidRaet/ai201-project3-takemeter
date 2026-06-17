# TakeMeter — planning.md

## Community Choice

**Community:**
<!-- Name the specific community (subreddit, Discord server, forum, etc.) -->

**Why this community fits the task:**
<!--
Explain — not just name — why this community is a good fit for discourse quality classification.
Consider: volume of takes, variance in quality, whether "good" vs "bad" takes have recognizable
features specific to this community, and whether the discourse is topical enough to have
consistent context. 2–4 sentences.
-->

***

## Label Taxonomy

<!--
Define 2–4 labels. Each label must:
- Be defined in a complete sentence (not a one-word description or vague adjective)
- Have clear boundaries from the other labels
- Include 2 example posts
- Address the hardest anticipated edge case between at least one pair of labels

Format per label:
-->

### Label 1: [NAME]

**Definition:**
<!-- Full sentence definition that specifies what qualifies and what does not. -->

**Examples:**
1. > <!-- Paste example post text here -->
2. > <!-- Paste example post text here -->

***

### Label 2: [NAME]

**Definition:**
<!-- Full sentence definition. -->

**Examples:**
1. > <!-- Paste example post text here -->
2. > <!-- Paste example post text here -->

***

### Label 3: [NAME] *(if applicable)*

**Definition:**
<!-- Full sentence definition. -->

**Examples:**
1. > <!-- Paste example post text here -->
2. > <!-- Paste example post text here -->

***

### Label 4: [NAME] *(if applicable)*

**Definition:**
<!-- Full sentence definition. -->

**Examples:**
1. > <!-- Paste example post text here -->
2. > <!-- Paste example post text here -->

***

## Hardest Anticipated Edge Case

**Label pair at issue:** <!-- e.g., Label A vs Label B -->

**Why this boundary is hard:**
<!--
Describe the type of post that genuinely sits between these two labels.
What features make it ambiguous? What rule or tiebreaker will you use to decide?
Be specific — name the characteristic, not just "it's hard to tell."
-->

**Resolution rule:**
<!-- The decision rule you will apply to cases that fall at this boundary. -->

***

## Data Collection Plan

**Source:**
<!-- Where the data is coming from (e.g., Reddit API via PRAW, manual scraping, existing dataset). -->

**Collection method:**
<!-- How you will pull the data — API, scraper, manual copy-paste, etc. Include any filters applied
(e.g., posts with >10 upvotes, posts from 2023–2024 only). -->

**Target volume:** <!-- e.g., 250 posts minimum -->

**Annotation process:**
<!--
How will you label each post? Who labels (just you, or with help from an LLM)?
If an LLM assists with pre-labeling, describe the workflow: prompt used, how you verified/corrected outputs.
-->

**Label distribution goal:**
<!--
How will you prevent any single label from exceeding 70% of the dataset?
e.g., collecting in batches per label, enforcing a cap, oversampling underrepresented labels.
-->

***

## Evaluation Metrics

**Chosen metrics:** <!-- e.g., per-class F1, macro-averaged F1, precision/recall per label, confusion matrix -->

**Reasoning:**
<!--
Why are these metrics appropriate for this task and label set?
If your labels are imbalanced, why does macro-F1 matter more than accuracy?
If the cost of false negatives differs by class, say so. 2–4 sentences.
-->

***

## Definition of "Good Enough"

<!--
State a concrete performance threshold — not "it should work well."
Example: "The fine-tuned model must achieve a macro-averaged F1 ≥ 0.70 on the held-out test set,
with no individual class F1 below 0.55."

Also note: how does this compare to the baseline? What would "good enough over baseline" look like?
-->

**Threshold:**

**Rationale:**
<!-- Why is this threshold meaningful for this specific classification task? -->

***

## AI Tool Plan

<!--
Describe at least one specific intended use of AI tools in this project.
Choose from: label stress-testing, annotation assistance, or failure pattern analysis.
Be specific about what you'll direct the model to do and how you'll verify or override its output.
-->

**Intended use(s):**

1. <!-- e.g., "Use an LLM to stress-test label definitions by generating adversarial examples that
   sit at the boundary between Label A and Label B, then revise definitions based on what breaks." -->

2. <!-- optional second use -->

**Oversight / override plan:**
<!-- How will you catch and correct AI errors, especially during annotation assistance? -->
