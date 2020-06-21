병렬 연산을 위해서 각 문서의 길이를 동일하게 맞춰주는 작업: </br>

example:</br>

```python
import numpy as np
from tensorflow.keras.preprocessing.text import Tokenizer
sentences = [['barber', 'person'], ['barber', 'good', 'person'], ['barber', 'huge', 'person'], ['knew', 'secret'], ['secret', 'kept', 'huge', 'secret'], ['huge', 'secret'], ['barber', 'kept', 'word'], ['barber', 'kept', 'word'], ['barber', 'kept', 'secret'], ['keeping', 'keeping', 'huge', 'secret', 'driving', 'barber', 'crazy'], ['barber', 'went', 'huge', 'mountain']]
tokenizer = Tokenizer()
tokenizer.fit_on_texts(sentences)
encoded = tokenizer.texts_to_sequences(sentences)
print(encoded)
```

Result: </br>
[[1, 5], [1, 8, 5], [1, 3, 5], [9, 2], [2, 4, 3, 2], [3, 2], [1, 4, 6], [1, 4, 6], [1, 4, 2], [7, 7, 3, 2, 10, 1, 11], [1, 12, 3, 13]]</br>

Words are changed into integers. To match the size:

```python
max_len = max(len(item) for item in encoded)
print(max_len)
for item in encoded: # 각 문장에 대해서
    while len(item) < max_len:   # max_len보다 작으면
        item.append(0)

padded_np = np.array(encoded)
padded_np
```

Result: </br>
array([[ 1,  5,  0,  0,  0,  0,  0],</br>
       [ 1,  8,  5,  0,  0,  0,  0],</br>
       [ 1,  3,  5,  0,  0,  0,  0],</br>
       [ 9,  2,  0,  0,  0,  0,  0],</br>
       [ 2,  4,  3,  2,  0,  0,  0],</br>
       [ 3,  2,  0,  0,  0,  0,  0],</br>
       [ 1,  4,  6,  0,  0,  0,  0],</br>
       [ 1,  4,  6,  0,  0,  0,  0],</br>
       [ 1,  4,  2,  0,  0,  0,  0],</br>
       [ 7,  7,  3,  2, 10,  1, 11],</br>
       [ 1, 12,  3, 13,  0,  0,  0]])</br>
