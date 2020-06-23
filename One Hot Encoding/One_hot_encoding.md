원-핫 인코딩은 단어 집합의 크기를 벡터의 차원으로 하고, 표현하고 싶은 단어의 인덱스에 1의 값을 부여하고, 다른 인덱스에는 0을 부여하는 단어의 벡터 표현 방식.
이 벡터를 One Hot Vector라고 부름. </br>
Example:

```python
from konlpy.tag import Okt  
okt=Okt()  
token=okt.morphs("나는 자연어 처리를 배운다")  
word2index={}
for voca in token:
     if voca not in word2index.keys():
       word2index[voca]=len(word2index)
       
def one_hot_encoding(word, word2index):
       one_hot_vector = [0]*(len(word2index))
       index=word2index[word]
       one_hot_vector[index]=1
       return one_hot_vector

```

위와 같이 One Hot Encoding을 구현해보았다. 
이를 테스트 해보면: </br>

```python
one_hot_encoding("자연어",word2index)
```

Result: </br>
[0, 0, 1, 0, 0, 0]  </br>

'자연어'라는 토큰을 [0,0,1,0,0,0]이라는 벡터로 변환하는 것을 확인.
