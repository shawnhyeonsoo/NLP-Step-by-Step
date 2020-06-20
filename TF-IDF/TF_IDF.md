libraries to use: sklearn

```python
from sklearn.feature_extraction.text import CountVectorizer
corpus = [
    'you know I want your love',
    'I like you',
    'what should I do ',    
]
vector = CountVectorizer()
print(vector.fit_transform(corpus).toarray()) 
print(vector.vocabulary_)
```

</br>
Result:</br>
[[0 1 0 1 0 1 0 1 1]</br>
 [0 0 1 0 0 0 0 1 0]</br>
 [1 0 0 0 1 0 1 0 0]]</br>
 {'you': 7, 'know': 1, 'want': 5, 'your': 8, 'love': 3, 'like': 2, 'what': 6, 'should': 4, 'do': 0}</br>


</br>
Now the TF-IDF part: </br>

```python
from sklearn.feature_extraction.text import TfidfVectorizer
corpus = [
    'you know I want your love',
    'I like you',
    'what should I do ',    
]
tfidfv = TfidfVectorizer().fit(corpus)
print(tfidfv.transform(corpus).toarray())
print(tfidfv.vocabulary_)
```

</br>
Result: </br>
[[0.         0.46735098 0.         0.46735098 0.         0.46735098 0.         0.35543247 0.46735098]</br>
 [0.         0.         0.79596054 0.         0.         0.         0.         0.60534851 0.        ]</br>
 [0.57735027 0.         0.         0.         0.57735027 0.         0.57735027 0.         0.        ]]</br>
{'you': 7, 'know': 1, 'want': 5, 'your': 8, 'love': 3, 'like': 2, 'what': 6, 'should': 4, 'do': 0}
