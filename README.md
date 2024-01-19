# Overview of Repository and Methodology

- Our codes are in "hw_score_predict.ipynb" file

  ## Methodology

  1. PreProcess
 - We applied pre-processing to all functions that were already available to us which were "prompts", "code2convos", "code2prompts", and "questions".  We applied stemming methods which we learned throughout the semester to each of the outputs of these functions. Also, in code2convos and code2prompts functions, name of the user and the chatgpt were seen in the html files which prevented us to apply stemming for some reason. So we removed those titles from the data and separated the prompts of the user and the responses of the chatgpt. After all these steps, we had each prompt of the user, each response of chatgpt to each prompt and all questions pre-processed and ready to be used in upcoming steps (i.e. finding similarity coefficients or applying statistics.)

  2. Extracted Features

     2.1 Features based on Prompt Matching.

  - Upon reflection, we recognized the limitations of utilizing similarity sums for grading purposes. Our approach involved calculating the summed similarity coefficient for each question per student and subsequently scaling the values. The scaling aimed to assign the highest grade to the maximum coefficient and zero points to the minimum coefficient. However, upon reviewing the resulting grades for each question across all students, we determined that this method was not suitable for our specific case.The reason why we concluded that is because when we sum the similarity across columns (so summation of similarity of a question with each prompt), the result tends to get much bigger for some students which is likely to mislead the end result. .Consequently, we decided not to pursue it any further.
  - Subsequently, we shifted our focus to choosing the maximum similarity of each question with the corresponding prompts. In this process, considering a set of 14 prompts for each user, we calculated 14 correlation coefficients for every question. The resulting table provided us with a range of similarity values for each question across the prompts. We then identified the maximum similarity for each question and student, storing this information in an array.To enhance interpretability, we normalized these similarity coefficients, scaling them between 0 and 1. Leveraging the scaled factors, we assigned a grade to each question for every student. Upon reviewing the grades, we found them to be meaningful and valuable. Subsequently, we aggregated the grades for each question and computed the final grade for each student. This final grade, seemed reasonable and indicative, was then incorporated as a distinctive feature in our approach.In total, we integrated nine features from this methodology, including eight similarity coefficients corresponding to eight questions and one final grade.

    2.2 Features based on statistics of the prompt.

  - prompt_avg_words : Average number of words in the chatgpt user prompt
  - response_avg_words: Average number of words in the chatgpt response
  - prompt_unique_words : Number of unique words in the user prompt
  - response_unique_words : Number of unique words in the chatgpt response
  - total_positive_words : Total number of positive words in the user prompt. We used opinion_lexicon to decide whether if its a positive word or not
  - total_negative_words: : Total number of negative words in the user prompt. We used opinion_lexicon to decide whether if its a negative word or not
  - longest_word_length : number of characters in the longest word
  - total_words : Summation of total_prompt_words and total_response_words.

![Feature Table](/images/Feature-Table.png)

# Results
## Before any features are added

| MSE Train         | MSE TEST           | R2 Train           | R2 Test                |
| ----------------- | ------------------ | ------------------ | ---------------------- |
| 2.667084370186041 | 112.21508237217598 | 0.9836796060156004 | 0.00044998314554067775 |

## Before prompt matching features are added(Only statistical features)

| MSE Train         | MSE TEST           | R2 Train           | R2 Test             |
| ----------------- | ------------------ | ------------------ | ------------------- |
| 3.742677139584356 | 173.98013101536912 | 0.9770978503127887 | -0.5497189790583146 |

## After all features are added

| MSE Train | MSE TEST | R2 Train | R2 Test            |
| --------- | -------- | -------- | ------------------ |
| 0.0       | 2.6      | 1.0      | 0.9768406350654163 |



# Team contributions
