Tokenizing with Keras:
example:

```python
from tensorflow.keras.preprocessing.text import Tokenizer
t  = Tokenizer()
fit_text = "The earth is an awesome place live"
t.fit_on_texts([fit_text])

test_text = "The earth is an great place live"
sequences = t.texts_to_sequences([test_text])[0]

print("sequences : ",sequences) 
print("word_index : ",t.word_index) # Vocabulary set
```


Result: </br>
sequences :  [1, 2, 3, 4, 6, 7] </br>
word_index :  {'the': 1, 'earth': 2, 'is': 3, 'an': 4, 'awesome': 5, 'place': 6, 'live': 7}
