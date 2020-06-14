# 1. Singular Value Decomposition: </br>
입력 행렬 A (m x n)를 다음과 같이 정의:
A=U Σ V<sup>T</br>
</br>
</br>
Document 1: "먹고 싶은 사과" </br>
Document 2: "먹고 싶은 바나나" </br>
Document 3: "바나나 길고 노란 바나나" </br>
Document 4: "저는 과일이 좋아요" </br>

이를 DTM으로 만든 후, 각 행렬로 분해:  </br>

```python
import numpy as np
A=np.array([[0,0,0,1,0,1,1,0,0],[0,0,0,1,1,0,1,0,0],[0,1,1,0,2,0,0,0,0],[1,0,0,0,0,0,0,1,1]])
np.shape(A)
U, s, VT = np.linalg.svd(A, full_matrices = True) #s는 Σ 의미
print(U.round(2))
np.shape(U)
```

여기서 s 는 특이값의 리스트: s.shape --> (4,)
이를 위해 제대로 된 행렬 모양의 Σ를 위해서 다음과 같이 실행:

```python
S = np.zeros((4, 9)) # 대각 행렬의 크기인 4 x 9의 임의의 행렬 생성
S[:4, :4] = np.diag(s) # 특이값을 대각행렬에 삽입
print(S.round(2))
np.shape(S)
```

Output: </br>
[[2.69 0.   0.   0.   0.   0.   0.   0.   0.  ]</br>
 [0.   2.05 0.   0.   0.   0.   0.   0.   0.  ]</br>
 [0.   0.   1.73 0.   0.   0.   0.   0.   0.  ]</br>
 [0.   0.   0.   0.77 0.   0.   0.   0.   0.  ]] </br>
 (4,9)

# 2. Truncated SVD
Let t = 2
```python
S=S[:2,:2]
#print(S.round(2))
U=U[:,:2]
#print(U.round(2))
VT=VT[:2,:]
#print(VT.round(2))
A_prime=np.dot(np.dot(U,S), VT)
print(A_prime.round(2))
```

Output: </br>
[[ 0.   -0.17 -0.17  1.08  0.12  0.62  1.08 -0.   -0.  ]</br>
 [ 0.    0.2   0.2   0.91  0.86  0.45  0.91  0.    0.  ]</br>
 [ 0.    0.93  0.93  0.03  2.05 -0.17  0.03  0.    0.  ]</br>
 [ 0.    0.    0.    0.    0.   -0.    0.    0.    0.  ]]
 
