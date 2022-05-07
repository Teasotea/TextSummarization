# *Abstractive Text Summarization*
Abstractive Text Summarization for psychological session notes

## Task
The task was to generate a summary of the given text in the form of key message bullet points. Allow the user to select how many bullets points to display (at least 3 to 7 bullet points) and adjust the length of them.

## Text Ranking and Paraphrasing Approach Details
 1) Preprocess text: remove stop words, words-parasites, numbers, punctuation, and symbols
 2) Build Vector Representations of sentences with SentenceTransformer `Distiluse-base-multilingual-cased`
 3) Build a similarity matrix (using cosine similarity) and rank sentences by their importance in the context 
 4) Use Paraphrasing Transformer Models to make sentences more readable for the end-user:
 `rugpt3large_based_on_gpt2` and `RUT5-base-paraphraser`. Choose the last one, because it shows the best performance
 5) Visualise and compare results with human-made summaries, which could be found here:  ([nbviewer](https://raw.githubusercontent.com/Teasotea/textSummarization/main/data/evaluation_summary_all.txt)) with ROUGE metric

### How to use:

```
summarize_text(text, remove_stop_words = True, num_bull_points=5, len_of_point=50, is_dialog = False)

```
The function preprocesses the text, then builds vector representations of sentences ranks them, and paraphrases.
The user can choose the number of final bullet points and their length

```
Parameters:
*remove_stop_words* - allows the user to choose whether to preprocess sentences or not
*num_bull_points* - the number of bullet points
*len_of_point* - max length of each bullet point
*is_dialog* - tells whether there is a necessity to parse psychologist's and client's replies separately

Returns: Pandas DataFrame
```
### Results:

![](https://github.com/Teasotea/textSummarization/blob/main/img/res.png?raw=true)

## Transformers Summarizer and Text Ranking Approach Details
 1) Launch pre-trained Transformer Summarizing models, compare their performance:
   * Bert2bert Model `rubert-base-cased`
   * T5 pre-trained on Telegram dataset `rut5-base`
   * T5 pre-trained on Gazeta.ru dataset `rut5-base` <br />
 <br />
 T5 pre-trained on the Telegram dataset model shows the best result.
 2) Build Vector Representations of sentences with SentenceTransformer `Distiluse-base-multilingual-cased`
 3) Build a similarity matrix (using cosine similarity) and rank sentences by their importance in the context 
 4)  Analyze and compare results with human-made summaries, which could be found here:  ([nbviewer](https://raw.githubusercontent.com/Teasotea/textSummarization/main/data/evaluation_summary_all.txt)) with ROUGE metric

### How to use:

```
summarize_text(text, num_bull_points=5, is_dialog = False)
```

The function summarizes key points from sentences with T5 Model, then builds vector representations of sentences, ranks them, and chooses the top results.
The user can choose the number of final bullet points.

```
Parameters:
*num_bull_points* - the number of bullet points
*is_dialog* - tells whether there is a necessity to parse psychologist's and client's replies separately

Returns: list of tuples
```


### Notebooks
- [`SentRanking.ipynb`](https://github.com/Teasotea/textSummarization/blob/main/SentRanking.ipynb) ([nbviewer](https://github.com/Teasotea/textSummarization/blob/main/SentRanking.ipynb)) - Notebook with Text Ranking and Paraphrasing Approach 
- [`Transformers.ipynb`](https://github.com/Teasotea/textSummarization/blob/main/Transformers.ipynb) ([nbviewer](https://github.com/Teasotea/textSummarization/blob/main/Transformers.ipynb)) - Notebook with Transformers Summarizer and Text Ranking Approach


### Some ideas for approach improvements

*   Explore dataset (EDA): do linguistical and statistical analysis, for example, word frequency calculation, normalization, considering the priority of words in a language. Fine research on that topic is in this [article](https://www.ijert.org/research/text-summarizer-using-abstractive-and-extractive-method-IJERTV3IS050821.pdf )
*   Develop text summarization solution using RNNs and LSTM (the core idea explained [here](https://www.analyticsvidhya.com/blog/2019/06/comprehensive-guide-text-summarization-using-deep-learning-python/ )) and compare the results
*   Improve Text Preprocessing: do the plural resolution, abbreviation resolution, synonym resolution, and remove personal information, like names, cities, and so on with the help of the NER model
*   Fine-Tune Transformers on the custom dataset, which consists of psychological sessions recordings
