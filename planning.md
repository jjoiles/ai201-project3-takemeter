# TakeMeter Project Planning

## Community

For this project, I chose the r/LetsTalkMusic community on Reddit. This community focuses on discussions about music, including artists, albums, songs, genres, production, and trends. I chose this community because the discussions contain a variety of responses, ranging from detailed analysis to personal opinions and short emotional reactions. This variety makes the community a good fit for a text classification task.

## Labels

### Analysis
A post or comment that makes a reasoned argument about music and supports the argument with specific details, examples, comparisons, or evidence.

Examples:
1. "The album's production feels more cohesive because the drums and bass are mixed more clearly than on their previous release."
2. "The artist's shift toward electronic production reflects the influence of synth-pop that can also be heard throughout their earlier work."

### Opinion
A post or comment that expresses a personal judgment or viewpoint about music and may provide some explanation, but does not develop a detailed argument.

Examples:
1. "I think this is their best album because the songs feel much more consistent."
2. "This artist is talented, but I prefer the sound of their earlier albums."

### Reaction
A post or comment that primarily expresses an immediate feeling, preference, praise, dislike, or emotional response with little to no reasoning.

Examples:
1. "This album is amazing!"
2. "I can't stand this song."

## Hard Edge Cases

The most difficult cases will likely be comments that contain both an opinion and some supporting information. For example, a person might say, "This is their best album because the production is much cleaner." This contains an opinion as well as a reason.

My decision rule will be based on the amount and specificity of the supporting reasoning. If the comment develops its claim using specific evidence, examples, comparisons, or detailed reasoning, I will classify it as `analysis`. If it mainly expresses a personal judgment with only a brief explanation, I will classify it as `opinion`. If it primarily expresses an emotional response with little or no explanation, I will classify it as `reaction`.

## Data Collection Plan

I will collect at least 200 public posts or comments from r/LetsTalkMusic. I will aim for a relatively balanced dataset with approximately 65-70 examples for each of the three labels.

The dataset will be stored in one CSV file with the columns `text`, `label`, and `notes`. The notes column will be used to document examples that are difficult to classify.

After collecting and labeling the examples, I will review the label distribution. If one label is underrepresented, I will collect additional examples that fit that label so that the model has enough examples from each category.

## Evaluation Metrics

I will evaluate the classifier using overall accuracy as well as precision, recall, and F1 score for each label. Accuracy will show the percentage of test examples that the model classifies correctly. However, accuracy alone may hide poor performance on an individual class, so the per-class metrics will help determine whether the model performs consistently across analysis, opinion, and reaction.

I will also use a confusion matrix to determine which labels are most frequently confused with each other. The fine-tuned model's results will be compared with the zero-shot Groq baseline on the same test set.

## Definition of Success

I will consider the classifier successful if it achieves at least 70% overall accuracy and approximately 0.70 F1 or higher across the three labels. I will also look for reasonably balanced performance between the labels rather than high performance on only one category.

For a real community tool, I would want the classifier to consistently distinguish detailed analysis from general opinions and short reactions without heavily favoring one label.

## AI Tool Plan

### Label Stress-Testing
I will use ChatGPT to generate example music comments that fall near the boundaries between analysis, opinion, and reaction. I will use these examples to test whether my label definitions and decision rules are clear enough before labeling the full dataset.

### Annotation Assistance
I may use ChatGPT to assist with identifying possible labels for difficult examples. However, I will personally review the examples and make the final labeling decision using the definitions established in this planning document.

### Failure Analysis
After evaluating the fine-tuned model, I will use ChatGPT to help identify patterns among incorrect predictions, such as whether the model struggles with short comments, ambiguous language, or specific pairs of labels. I will verify any identified patterns by reviewing the incorrect predictions myself.
