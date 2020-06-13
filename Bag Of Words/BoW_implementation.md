한국어 예제를 통한 실습: </br>
문장: 정부가 발표하는 물가상승률과 소비자가 느끼는 물가상승률은 다르다.
</br>
</br>

```python
from konlpy.tag import Okt
import re  
okt=Okt()  
token=re.sub("(\.)","","정부가 발표하는 물가상승률과 소비자가 느끼는 물가상승률은 다르다.") 
#온점 제거 작업
token=okt.morphs(token)
#token화 작업 완료
word2index={}  
bow=[]  #Bag of Words
for voca in token:  
         if voca not in word2index.keys():  
             word2index[voca]=len(word2index)  # token을 단어 단위로 흝으면서, word2index에 없는 단어는 새로 추가하고, 이미 있는 단어는 pass   
             bow.insert(len(word2index)-1,1) # bow.insert 함수로 BoW에 들어갈 각 단어 항목에 숫자 '1' 을 추가하면서 시작.
         else:
            index=word2index.get(voca) # 재등장하는 단어의 인덱스 찾기
            bow[index]=bow[index]+1 # 재등장한 단어는 해당하는 인덱스의 위치에 1을 add (frequency 가 1 이상)
print(word2index)  
print(bow)
```

Output: </br>
{'정부': 0, '가': 1, '발표': 2, '하는': 3, '물가상승률': 4, '과': 5, '소비자': 6, '느끼는': 7, '은': 8, '다르다': 9} </br>
[1, 2, 1, 1, 2, 1, 1, 1, 1, 1]</br>

이를 표로 만들면:

|Word| Frequency|
|--|---|
|정부|1|
|가|2|
|발표|1|
|하는|1|
|물가상승률|2|
|과|1|
|소비자|1|
|느끼는|1|
|은|1|
|다르다|1|
