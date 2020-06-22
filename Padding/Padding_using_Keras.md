Keras supports padding tool: "pad_sequences()"
example:

```python
from tensorflow.keras.preprocessing.sequence import pad_sequences
sentences = [['barber', 'person'], ['barber', 'good', 'person'], ['barber', 'huge', 'person'], ['knew', 'secret'], ['secret', 'kept', 'huge', 'secret'], ['huge', 'secret'], ['barber', 'kept', 'word'], ['barber', 'kept', 'word'], ['barber', 'kept', 'secret'], ['keeping', 'keeping', 'huge', 'secret', 'driving', 'barber', 'crazy'], ['barber', 'went', 'huge', 'mountain']]
encoded = tokenizer.texts_to_sequences(sentences)
print(encoded)
```

Result: </br>
[[1, 5], [1, 8, 5], [1, 3, 5], [9, 2], [2, 4, 3, 2], [3, 2], [1, 4, 6], [1, 4, 6], [1, 4, 2], [7, 7, 3, 2, 10, 1, 11], [1, 12, 3, 13]]


```python
padded = pad_sequences(encoded)
padded
```

Result: </br>
array([[ 0,  0,  0,  0,  0,  1,  5],</br>
       [ 0,  0,  0,  0,  1,  8,  5],</br>
       [ 0,  0,  0,  0,  1,  3,  5],</br>
       [ 0,  0,  0,  0,  0,  9,  2],</br>
       [ 0,  0,  0,  2,  4,  3,  2],</br>
       [ 0,  0,  0,  0,  0,  3,  2],</br>
       [ 0,  0,  0,  0,  1,  4,  6],</br>
       [ 0,  0,  0,  0,  1,  4,  6],</br>
       [ 0,  0,  0,  0,  1,  4,  2],</br>
       [ 7,  7,  3,  2, 10,  1, 11],</br>
       [ 0,  0,  0,  1, 12,  3, 13]], dtype=int32)</br>

It can be seen that shapes are a little different from that of numpy: this is because pad_sequences puts 0's at the front.
