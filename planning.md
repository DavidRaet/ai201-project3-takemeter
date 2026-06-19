# TakeMeter - planning.md

## Community Choice

**Community:**
Reddit (r/soccer)

**Why this community fits the task:**

The soccer subreddit is a diverse and large dataset for classifying all sorts of comments. r/soccer is a link-heavy subreddit where comment threads, particularly match threads and debate posts, provide the richest source of labeled discourse (Hot Takes, Reactions, Arguments, Analyses), making comments the primary collection unit.

***

## Label Taxonomy

### Label 1: Hot Take

**Definition:**

A hot take can be defined as a novel claim with the potential to spark debate, but has little to no perceived backing of evidence, data, or logical reasoning. This can come in the form of an overall statement about a footballer such as: "This player doesn't have what it takes to be a world-class player," and proceeds to not elaborate on why that person thinks so. More examples can be seen below:


**Key Indicator:** The post asserts an opinion as a fact but provides no "why" or supporting stats.

**Examples:**
1. > "Ronaldo is too old to win the World Cup with Portugal." (Opinion, no stats on his current form).
2. > "Lamine Yamal will be our next generations GOAT, comparable to Ronaldo and Messi." (Prediction without trajectory data).

***

### Label 2: Analysis

**Definition:**
An analysis can be defined as an objective description of events, statistics, or situations. This type of statement will often not take any sides, and will be supported from observation, evidence, and fact. 

**Key Indicator:** The post could be verified as true or false by a match report or database. It contains no persuasive language.

**Examples:**
1. > "Messi was able to score a hattrick against Algeria, ending the game with a score of 3-0."
2. > "Japan was able to tie against The Netherlands with a score of 2-2 as Kamada scores the final goal of the match in the 89th minute." 

***

### Label 3: Argument

**Definition:**
An argument is a claim that has the subjectivity of a hot take that is supported with concrete evidence, data, or logical reasoning like an analysis. 

**Key Indicator:** The post follows the structure: **Claim + Evidence + Conclusion**. The evidence must be specific (e.g stats, dates, historical context).

**Examples:**
1. > "Lamine Yamal will be our next generations GOAT, comparable to Ronaldo and Messi because of his trajectory. At 18 years and 7 months, Lamine Yamal has accumulated 100 combined goals and assists for Barcelona and Spain. At the exact same age, Messi had 5 goal contributions total, Ronaldo had 4, and Mbappé, widely considered the best of this current generation before Yamal arrived, was 60 behind that mark. We are watching an unprecedented statistic that has never existed in this age of top-flight football."
2. > "Messi is the undisputed GOAT of football because of many factors. He holds La Liga's all-time records for most goals (474), most goals in a single season (50), and most hat-tricks (36). He's an 8-time Ballon d'Or winner, with Ronaldo being second to him with 5. Despite the past counter-argument for his lack of international trophies, Messi dismantled it completely by winning the 2021 Copa América, the Finalissima, and the 2022 FIFA World Cup." 

***

### Label 4: Reaction

**Definition:**


A reaction is a subjective expression of emotion, shock, or personal feeling regarding an event. It does not make a universal claim or argument.

**Key Indicator:** The post describes *how the user feels* rather than *what is true*. Often includes emojis, exclamations, or rhetorical questions.

**Examples:**
1. > "Messi just scored an insane banger of a goal."
2. > "What did I just witness? 😭"
3. > "I can't believe the ref missed that call."
***

## Hardest Anticipated Edge Case

**Label pair at issue:** When a comment seems to have a mix of different types of labels. For example, a comment like "Messi just scored an insane banger of a goal. This is why he's the GOAT," could have a mix of a reaction and a hot take.  

**Why this boundary is hard:**
The reason why this boundary is hard to classify is because a comments intention is difficult to read and thus can't be placed in one specific label.

**Resolution rule:**
To counteract this anticipated edge case, we will use a Dominant Intent Heuristic to concretely classify a comment with an amibigious label. This approach will look at the comments final conclusion, which will determine the label. When a comment appears to have a mixed signal like the initial example mentioned, "Messi just scored an insane banger of a goal. This is why he's the GOAT," this comment will be labeled as a hot take as the comment's last sentence was driven by a sentiment that can be regelated in that category.

However, because we are classifying comments with dual intent into one category using the Dominant Intent Heuristic, some tradeoffs with this approach include:

- Loss of Nuance: Comments with a balanced, dual-intent are forced into one category, which strips the wholistic message of the user.
- Ambiguity in Sarcasm: Sarcasm has the possibility of flipping the dominant intent. (e.g "Messi scored a hattrick? Yeah right... He's the GOAT.")
- Simplified Metrics: The accuracy could be shown nicely since the model is learning the most common patterns, but it's also possible that the model could have confused two labels at some point. 

***

## Data Collection Plan

**Source:**
Implementation will use PRAW for data ingestion and will target the soccer subreddit (r/soccer)

**Collection method:**
We collect the data using a variety of filters:

- Time Range: Filter by posts in the last 5 years to ensure modern discourse content. 
- Engagement Threshold: Filter comments with a score of >= 5 to mitigate chances of a discourse being spam or low-effort noise. 
- Content Type: Include comments from high-engagement threads (match threads, discussion posts, hot takes threads) and exclude posts that are less than 20 words in length to ensure sufficient context for classification. (including title and body) 
- Exclusions: Filter out posts from banned users or posts marked as "NSFW" as we are targetting general quality posts. 
- Rate Limiting: Use PRAW's built-in rate limiting. 

**Target volume:** 2500 posts.

**Annotation process:**
<!--
How will you label each post? Who labels (just you, or with help from an LLM)?
If an LLM assists with pre-labeling, describe the workflow: prompt used, how you verified/corrected outputs.
-->
Posts will be labeled using a Hybrid LLM-Assisted Pre-Labeling with Human Verification approach. 

**Workflow:**
1.  **Rubric Creation:** We will define specific criteria for discourse quality with explicit examples.
2.  **Pre-Labeling:** An LLM will process the dataset using a few-shot prompt containing:
    *   The discourse quality rubric.
    *   5 examples of posts with correct labels and reasoning.
    *   The target comment text.
    *   *Output format:* JSON with `text`, `label`, `reasoning`, and `confidence_score`.
3.  **Human-in-the-Loop Verification:**
    *   **Low Confidence (<0.85):** Automatically flagged for manual review.
    *   **High Confidence:** A random 15% sample will be manually audited.
    *   Any systematic errors found in the audit will trigger a prompt refinement cycle.
4.  **Final Dataset:** The corrected dataset will be used to fine-tune the `TakeMeter` classifier.



**Label distribution goal:**
<!--
How will you prevent any single label from exceeding 70% of the dataset?
e.g., collecting in batches per label, enforcing a cap, oversampling underrepresented labels.
-->
To prevent any single label from exceeding a high percentage of the dataset, we will use a two-stage filtering approach. 

1. Pre-Labeling Heuristic Filter:

   - Before LLM processing, we will filter out obvious noise (e.g., posts with <15 words, pure image posts, or posts with >90% stop-words). This reduces the "Off-Topic" volume at the source, saving API costs and time.

2. Post-Labeling Undersampling:

   - After LLM labeling, if a class still exceeds the 70% threshold, we will perform Random Undersampling on that specific class. The high-level logic looks like: 
      target_count = total_posts * 0.65. 
      If class_count > target_count, randomly drop the excess. 
      For safety, We will maintain a backup of the dropped data in case we need to retrain with a larger dataset later.

***

## Evaluation Metrics

**Chosen metrics:** Macro-Averaged F1-Score as the primary headline metric, supported by a Confusion Matrix and Per-Class Recall.

**Reasoning:**

Social media discourse datasets like r/soccer are typically highly imbalanced, with "low effort" or "spam" content vastly outnumbering "high quality" discourse; Macro-F1 is essential here because it prevents the model from achieving a deceptively high score by simply predicting the majority class, ensuring the model actually learns to identify rare, valuable contributions. Additionally, in discourse evaluation, the cost of a False Negative (missing a high-quality discussion) is often higher than a False Positive (finding a low-quality discussion), making Per-Class Recall critical for ensuring the system captures the nuance it was designed to find. The Confusion Matrix is included to visually verify if the model is confusing semantically similar but distinct categories, such as "Hot Takes" vs. "Arguments," which simple aggregate scores would miss.

***

## Definition of "Good Enough"

<!--
State a concrete performance threshold — not "it should work well."
Example: "The fine-tuned model must achieve a macro-averaged F1 ≥ 0.70 on the held-out test set,
with no individual class F1 below 0.55."

Also note: how does this compare to the baseline? What would "good enough over baseline" look like?
-->

**Threshold:**

The fine-tuned model should have a macro-averaged F1 of greater than or equal to 0.70 on a held-out test set, with no indiviudal class F1 dropping below a 0.55. 


**Rationale:**

Since, Social media discourse datasets are notoriously imbalanced and noisy, a Macro-F1 ≥ 0.70 aligns with competitive benchmarks for fine-tuned 7B–8B LLMs on similar social media sentiment tasks, indicating the model has moved beyond random guessing and majority-class bias. However, because the primary goal of TakeMeter is to surface valuable discussions, an additional Per-Class Recall constraint of greater than or equal to 0.75 is critical to ensure we do not miss high-quality content (False Negatives), even if it slightly penalizes precision. The 0.55 floor for individual classes prevents the model from completely failing on minority categories (e.g., "Reactions" or "Hot Takes"), which would render the tool useless for nuanced moderation.

***

## AI Tool Plan

<!--
Describe at least one specific intended use of AI tools in this project.
Choose from: label stress-testing, annotation assistance, or failure pattern analysis.
Be specific about what you'll direct the model to do and how you'll verify or override its output.
-->

**Intended use(s):**

1. Label stress-testing: I plan to give the LLM my label definitions and edge case descriptions. Then, ask it to generate 5–10 posts that sit at the boundary between two labels. If it produces posts it can't classify cleanly, I will go back to the drawing board and tighten the definitions. 

2. Annotation assistance: I will use an LLM, specifically Claude 4.6 Sonnet, to pre-label a batch of examples before reviewing them yourself. Then, I will track which examples were pre-labeled (for disclosure in my AI usage section).

3. Failure analysis: I plan to give a list of wrong predictions to an LLM and ask it to identify patterns before asking to write up an evaluation. To verify the patterns I will give the LLM a list of failed predictions and ask it to identify about 3 recurring patterns causing them. Then, I step in to do a pattern verification that involves both a quantitative and qualitative step. On the quantitative step, extract the patterns that the LLM found and compare them in the failed set vs the correct set to individually see if these patterns hold. for the qualitative check, sample 10-15 instances and check if the LLM's explanation for the failed sets is accurate and the cause is the respective pattern. Lastly, on my eval report add these verified patterns and come up with mitigation strategies for the ones that the LLM may not have cleanly analyzed.

**Oversight / override plan:**
<!-- How will you catch and correct AI errors, especially during annotation assistance? -->
To catch and correct AI errors, I wll thoroughly review the LLM's output, carefully prompt with detailed and precise instructions using a Role-Task-Format model to handle delicate tasks like annotation assistance to lessen the risk of unfavorable outputs, and edit accordingly.