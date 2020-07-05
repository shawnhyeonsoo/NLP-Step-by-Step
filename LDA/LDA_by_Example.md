잠재 디리클레 할당 (Latent Dirichlet Allocation)  </br>

15년 동안 발행되었던 뉴스 기사 제목을 모아놓은 영어 데이터 다운 -> headline_text (뉴스 기사 제목) 분리 -> 전처리 (단어 토큰화, 불용어 제거, 표제어 추출, 길이 바탕 단어 제거) -> TF-IDF-> 토픽 모델링


Source Code (python):

```python
import pandas as pd
import urllib.request
import nltk
from sklearn.decomposition import LatentDirichletAllocation
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer
from sklearn.feature_extraction.text import TfidfVectorizer

urllib.request.urlretrieve("https://raw.githubusercontent.com/franciscadias/data/master/abcnews-date-text.csv", filename="abcnews-date-text.csv")
data = pd.read_csv('abcnews-date-text.csv', error_bad_lines=False)

text = data[['headline_text']]
text.head(5)
text['headline_text'] = text.apply(lambda row: nltk.word_tokenize(row['headline_text']), axis=1)

stop = stopwords.words('english')
text['headline_text'] = text['headline_text'].apply(lambda x: [word for word in x if word not in (stop)])

text['headline_text'] = text['headline_text'].apply(lambda x: [WordNetLemmatizer().lemmatize(word, pos='v') for word in x])

tokenized_doc = text['headline_text'].apply(lambda x: [word for word in x if len(word) > 3])


detokenized_doc = []
for i in range(len(text)):
    t = ' '.join(tokenized_doc[i])
    detokenized_doc.append(t)

text['headline_text'] = detokenized_doc # 다시 text['headline_text']에 재저장


vectorizer = TfidfVectorizer(stop_words='english',
max_features= 1000) # 상위 1,000개의 단어를 보존
X = vectorizer.fit_transform(text['headline_text'])
#X.shape # TF-IDF 행렬의 크기 확인

lda_model=LatentDirichletAllocation(n_components=10,learning_method='online',random_state=777,max_iter=1)

lda_top=lda_model.fit_transform(X)

terms = vectorizer.get_feature_names() # 단어 집합. 1,000개의 단어가 저장됨.

def get_topics(components, feature_names, n=5):
    for idx, topic in enumerate(components):
        print("Topic %d:" % (idx+1), [(feature_names[i], topic[i].round(2)) for i in topic.argsort()[:-n - 1:-1]])

get_topics(lda_model.components_,terms)
```

Output: </br>
Topic 1: [('government', 8725.19), ('sydney', 8393.29), ('queensland', 7720.12), ('change', 5874.27), ('home', 5674.38)]</br>
Topic 2: [('australia', 13691.08), ('australian', 11088.95), ('melbourne', 7528.43), ('world', 6707.7), ('south', 6677.03)]</br>
Topic 3: [('death', 5935.06), ('interview', 5924.98), ('kill', 5851.6), ('jail', 4632.85), ('life', 4275.27)]</br>
Topic 4: [('house', 6113.49), ('2016', 5488.19), ('state', 4923.41), ('brisbane', 4857.21), ('tasmania', 4610.97)]</br>
Topic 5: [('court', 7542.74), ('attack', 6959.64), ('open', 5663.0), ('face', 5193.63), ('warn', 5115.01)]</br>
Topic 6: [('market', 5545.86), ('rural', 5502.89), ('plan', 4828.71), ('indigenous', 4223.4), ('power', 3968.26)]</br>
Topic 7: [('charge', 8428.8), ('election', 7561.63), ('adelaide', 6758.36), ('make', 5658.99), ('test', 5062.69)]</br>
Topic 8: [('police', 12092.44), ('crash', 5281.14), ('drug', 4290.87), ('beat', 3257.58), ('rise', 2934.92)]</br>
Topic 9: [('fund', 4693.03), ('labor', 4047.69), ('national', 4038.68), ('council', 4006.62), ('claim', 3604.75)]</br>
Topic 10: [('trump', 11966.41), ('perth', 6456.53), ('report', 5611.33), ('school', 5465.06), ('woman', 5456.76)]</br>

> 사이킷런을 통해 LDA 실습을 해보았는데, 제공된 라이브러리를 이용하여 구현해보는 경험을 해볼 수 있었다. 앞서 해본 텍스트 전처리 와 TF-IDF 구현 등에 이어서 추가적으로 이러한 기법을
  구현해본다는 것 역시 큰 의미가 있으며, 이를 직접 구현해보면서 이론적으로 배운 것에 추가적으로 이해가 되는 부분 역시 있는 것 같다. 출처는 <딥러닝을 위한 자연어 처리 입문>으로, 
  https://wikidocs.net/book/2155 을 참고하여 작성하였음을 알립니다. 
