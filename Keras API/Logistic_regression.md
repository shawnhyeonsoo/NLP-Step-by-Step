An example implementation of logistic regression, using Keras.

```python
from tensorflow.keras.layers import Input, Dense
from tensorflow.keras.models import Model

inputs = Input(shape=(3,))
output = Dense(1, activation='sigmoid')(inputs)
logistic_model = Model(inputs, output)

logistic_model.compile(optimizer='sgd', loss = 'binary_crossentropy', metrics=['accuracy'])
logistic_model.optimizer.lr = 0.001
logistic_model.fit(x=dat_train, y=y_classifier_train, epochs = 5, validation_data = (dat_test, y_classifier_test))
```
