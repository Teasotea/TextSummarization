# Abstractive Text Summarization for psycological session notes

## Task
The task was to generate a summary of given text in the form of key message bullet points. Allow the user to select how many bullet points to display (at least from 3 to 7 bullet points) and adjust the length of them.

## Main Approach Details
 1) Preprocess text: remove stop words, words-parasites, numbers, punctuation and symbols
 2) Perform Vector Representation of Sentences with SentenceTransformer `Distiluse-base-multilingual-cased`
 3) Build similarity matrix and rank sentences by their importance to context
 4) Use Paraphrasing Transformer Models to makesentences more redable for the end-user:
 `rugpt3large_based_on_gpt2` and `RUT5-base-paraphraser`. Choose the last one, thus it shows the best perfomance
 6) Visualise and compare results with human-made summaries, that could be found here:  ([nbviewer](https://raw.githubusercontent.com/Teasotea/textSummarization/main/data/evaluation_summary_all.txt)) with ROUGE metric

## Additional Approach Details
Ready-to-use solutions with pretrained transformers:
   * Bert2bert Model `rubert-base-cased`
   * T5 pretrained on Telegram dataset `rut5-base`
   * T5 pretrained on Gazeta.ru dataset `rut5-base`
T5 pretrained on Telegram dataset model has shown the best results. Hence, it 
could be further ranked using the steps descibed above and get ready to use by selecting most-ranked sentences

## Results

![](https://github.com/Teasotea/textSummarization/blob/main/img/results.png?raw=true)
![](https://github.com/Teasotea/textSummarization/blob/main/img/res.png?raw=true)

## Notebooks
- [`SentRanking.ipynb`](https://github.com/Teasotea/textSummarization/blob/main/SentRanking.ipynb) ([nbviewer](https://github.com/Teasotea/textSummarization/blob/main/SentRanking.ipynb)) - Notebook with final solution
- [`Transformers.ipynb`](https://github.com/Teasotea/textSummarization/blob/main/Transformers.ipynb) ([nbviewer](https://github.com/Teasotea/textSummarization/blob/main/Transformers.ipynb)) - Notebook with the simple solution based on pretrained transformers


### Possible Improvements

  * Explore dataset (EDA): do linguistical and statistical analysis, for example word frequency calculation, normalization, consider priority of words in language
  * Try RNN and LSTM Architechtures and compare the results
  * Improve Text Preprocessing: do plural resolution, abbreviation resolution, synonimum resolution and remove personal information, like: names, cities and so on with the help of NER model
  * Fine-Tune Transformers on custom dataset, which consists of psycological sessions recordings


