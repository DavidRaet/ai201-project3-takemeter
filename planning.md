# TakeMeter — planning.md

## Community Choice

**Community:**
Reddit (r/soccer)

**Why this community fits the task:**
<!--
Explain — not just name — why this community is a good fit for discourse quality classification.
Consider: volume of takes, variance in quality, whether "good" vs "bad" takes have recognizable
features specific to this community, and whether the discourse is topical enough to have
consistent context. 2–4 sentences.

The soccer subreddit is a diverse and large dataset for classifying all sorts of comments. Whether the comment is a simple reaction like, what a goal!, or a hot take, This soccer player is washed up 😭✌️, or an analysis like Messi just scored a hattrick against Algeria, we can recognize patterns in a sport that offers an abundant dataset for TakeMeter.  


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

### Label 1: Hot Take

**Definition:**

A hot take can be defined as a novel claim with the potential to spark debate, but has little to no perceived backing of evidence or fact. This can come in the form of an overall statement about a footballer such as: "This player doesn't have what it takes to be a world-class player," and proceeds to not elaborate on why that person thinks so. More examples can be seen below:

**Examples:**
1. > "Ronaldo is 40 years old. He is able to win the world cup with Portugal even with his given team and his current condition!"
2. > "Lamine Yamal will be our next generations GOAT, comparable to Ronaldo and Messi."

***

### Label 2: Analysis

**Definition:**
An analysis can be defined as a statement that describes a situation, person, and miscellaneous objects from an objective standpoint. This type of statement will often not take any sides, and will be supported from observation, evidence, and fact. 

**Examples:**
1. > "Messi was able to score a hattrick against Algeria, ending the game with a score of 3-0."
2. > "Japan was able to tie against The Netherlands with a score of 2-2 as Kamada scores the final goal of the match at the 89th minute." 

***

### Label 3: Argument

**Definition:**
An argument is a claim that has the zealous of a hot take mixed with the rigor of an analysis. Usually a person would propose their hot take and later on through an analysis, back up that hot take. 

**Examples:**
1. > "Lamine Yamal will be our next generations GOAT, comparable to Ronaldo and Messi because of his trajectory. At 18 years and 7 months, Lamine Yamal has accumulated 100 combined goals and assists for Barcelona and Spain. At the exact same age, Messi had 5 goal contributions total, Ronaldo had 4, and Mbappé, widely considered the best of this current generation before Yamal arrived, was 60 behind that mark. We are watching an unprecedented statistic that has never existed in this age of top-flight football. "
2. > "Messi is the undisputed GOAT of football because of many factors. He holds La Liga's all-time records for most goals (474), most goals in a single season (50), and most hat-tricks (36). He's an 8-time Ballon d'Or winner, with Ronaldo being second to him with 5. Despite the past counter-argument for his lack of international trophies, Messi dismantled it completely by winning the 2021 Copa América, the Finalissima, and the 2022 FIFA World Cup." 

***

### Label 4: Reaction

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
