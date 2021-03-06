
# Question Answering
<i><b>information retrieval</b></i>

---

## Advance preparation
1.Execute linux.sh or windows.bat to create config link<br>
2.Modify the variable root_path in src/config/path.py<br>
3.Put the data set in data folder

---

## Data set
document set: WF Cases 20190517.csv<br>
query set:    NABU FAQ for Worry Free Product 20190401.csv

---

## Preprocessing
### email_preprocess.py
Extract the main of email and remove garbage information.<br>
Finally output is a cPickle file.
### create_dictionary.py
Use the output file of email_preprocess.py to create dictionary.
### word2id.py
Use dictionary to transfer the word of email to word ID.

---

## Method
### Unigram Language Model
<i>Q:What is unigram language model?<br>
A:probability distribution over the words in a language.<br></i>

We use document and query to generate document language model and query language model, and then calculate KL-Divergence score to rank the relevant document.

<img src="http://latex.codecogs.com/gif.latex?\\ {KL(Q||D)}=\sum_{w\in{V}}\frac{f_{w,Q}}{|Q|}\log{P(w|D)}" />

<img src="http://latex.codecogs.com/gif.latex?\\ Q" /> is query, <img src="http://latex.codecogs.com/gif.latex?\\ D" /> is document, <img src="http://latex.codecogs.com/gif.latex?\\ w" /> is word, <img src="http://latex.codecogs.com/gif.latex?\\ V" /> is all of the vocabulary, <img src="http://latex.codecogs.com/gif.latex?\\ f_{w,Q}" /> is frequency of the word <img src="http://latex.codecogs.com/gif.latex?\\ w" /> in query <img src="http://latex.codecogs.com/gif.latex?\\ Q" />


### IR_qustion2qustion.py
We use the subject of "NABU FAQ for Worry Free Product 20190401.csv" as query, and the subject of "WF Cases 20190517.csv" as document. At the beginning of the code is LM generation, and then calculate the KL score between document LM and query LM. Finally, rank and select top N relevant subject to output<br> 
How to execute: email_preprocess.py -> create_dictionary.py -> word2id.py -> IR_qustion2qustion.py
### IR_prediction.py
It can predict one query which user input.<br> 
How to execute: email_preprocess.py -> create_dictionary.py -> word2id.py -> IR_prediction.py

---

## To do
IR_prediction.py GUI and show the simlarity value
