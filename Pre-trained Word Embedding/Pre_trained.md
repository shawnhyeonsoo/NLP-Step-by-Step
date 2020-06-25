Implementing using Keras: 

```python
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences
import numpy as np
sentences = ['nice great best amazing', 'stop lies', 'pitiful nerd', 'excellent work', 'supreme quality', 'bad', 'highly respectable']
y_train = [1, 0, 0, 1, 1, 0, 1]
t = Tokenizer()
t.fit_on_texts(sentences)
vocab_size = len(t.word_index) + 1
X_encoded = t.texts_to_sequences(sentences)
#print(X_encoded)
max_len=max(len(l) for l in X_encoded)
#print(max_len)
X_train=pad_sequences(X_encoded, maxlen=max_len, padding='post')
y_train=np.array(y_train)
print(X_train)
```

Result: </br>
[[ 1  2  3  4] </br>
 [ 5  6  0  0] </br>
 [ 7  8  0  0] </br>
 [ 9 10  0  0] </br>
 [11 12  0  0] </br>
 [13  0  0  0] </br>
 [14 15  0  0]] </br>

PreProcessing of training data complete:
Model: </br>

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Embedding, Flatten

model = Sequential()
model.add(Embedding(vocab_size, 4, input_length=max_len)) # 모든 임베딩 벡터는 4차원.
model.add(Flatten()) # Dense의 입력으로 넣기위함.
model.add(Dense(1, activation='sigmoid'))
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['acc'])
model.fit(X_train, y_train, epochs=100, verbose=2)
```

단어들의 임베딩 벡터들의 값은 학습 과정에서 다른 가중치들과 함께 학습된 값
