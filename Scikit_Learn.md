# Scikit-Learn

## sklearn 라이브러리를 통한 train_test_split
```python
from sklearn.model_selection import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(X,Y,test_size=0.2,random_state=30)
```

## sklearn 라이브러리를 통한 parameter check
- Grid Search
```python
from sklearn.model_selection import GridSearchCV
params = {'param':'check'}                        # {parameter:check하고 싶은 수치} 등록
clf = GridSearchCV(model, params)
clf.fit(X_train,y_train)
```
- Randomized Search
```python
from sklearn.model_selection import RandomizedSearchCV
params = {
    'n_estimators': randint(low=1, high=200),
    'max_features': randint(low=1, high=8)
}
clf = RandomizedSearchCV(model,params)
clf.fit(X_train,y_train)
cvres = clf.cv_result
for rank, param in zip(cvres['rank_test_score'],cvres['params']):
    print(f'{rank} : {param}')
print(clf.best_params_)
```

## sklearn 라이브러리를 통한 Linear Regression
```python
from sklearn.linear_model import LinearRegression
reg = LinearRegression(fit_intercept=True)          # y절편 생략 X
reg.fit(X,Y)
```

## sklearn 라이브러리를 통한 모델 평가
```python
from sklearn.metrics import accuracy_score, f1_score, precision_score, recall_score, roc_auc_score
def metrics(y_test, pred):
    accuracy = accuracy_score(y_test, pred)
    precision = precision_score(y_test, pred)
    recall = recall_score(y_test, pred)
    f1 = f1_score(y_test, pred)
    roc_score = roc_auc_score(y_test, pred)
    print('정확도 : {0:.2f}, 정밀도 : {1:.2f}, 재현율 : {2:.2f}'.format(accuracy, precision, recall))
    print('f1-score : {0:.2f}, auc : {1:.2f}'.format(f1, roc_score))
```

## K-Fold
```python
from sklearn.model_selection import KFold
kf = KFold(n_split=n, shuffle=False, random_state=10)
for train_index, test_index in kf.split(df) :
    train = df[train_index]
    test = df[test_index]
```