Sequential(): 케라스에서는 입력층, 은닉층, 출력층을 구성하기 위해 Sequential()을 사용.</br>
model로 선언한 뒤에 model.add()라는 코드를 통해 층을 단계적으로 추가.

example: </br>

```python
from tensorflow.keras.models import Sequential
model = Sequential()
model.add(...) # 층 추가
model.add(...) # 층 추가
model.add(...) # 층 추가
```

example: Embedding, Dense:

```python
from tensorflow.keras.models import Sequential
model = Sequential()
model.add(Embedding(vocabulary, output_dim, input_length))
```

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
model = Sequential()
model.add(Dense(1, input_dim=3, activation='relu'))
```

Dense(): </br>
input_dim = 입력 뉴런의 수. (입력의 차원)
activation = 활성화 함수.
- linear : 디폴트 값으로 별도 활성화 함수 없이 입력 뉴런과 가중치의 계산 결과 그대로 출력. Ex) 선형 회귀
- sigmoid : 시그모이드 함수. 이진 분류 문제에서 출력층에 주로 사용되는 활성화 함수.
- softmax : 소프트맥스 함수. 셋 이상을 분류하는 다중 클래스 분류 문제에서 출력층에 주로 사용되는 활성화 함수.
- relu : 렐루 함수. 은닉층에 주로 사용되는 활성화 함수.
