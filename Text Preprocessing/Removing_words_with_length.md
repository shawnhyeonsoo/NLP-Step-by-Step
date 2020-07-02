Words can be removed according to their lengths. 

Example: </br>

```python
import re
text = "I was wondering if anyone out there could enlighten me on this car."
shortword = re.compile(r'\W*\b\w{1,2}\b')
print(shortword.sub('', text))
```
Output: </br>
was wondering anyone out there could enlighten this car.

This example removes words with length 1~2. For example, words such as 'I', 'if', 'me' are removed.
