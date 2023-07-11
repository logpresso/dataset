# dataset
Public dataset for tutorial

## wp-nginx

### csv

```
wget url="https://raw.githubusercontent.com/logpresso/dataset/main/wp-nginx.csv"
| eval line = subarray(split(line, "\n"), 1) | explode line 
| parsecsv date,login,logtype,referer,remote_host,request,sent,status,user,user_agent
| rename date as _time | order _time
| eval remote_host=ip(remote_host), sent=int(sent), status=int(status), _time=date(_time, "EEE MMM dd HH:mm:ss z yyyy")
```

## iris

```
wget url="https://raw.githubusercontent.com/logpresso/dataset/main/iris.csv" | eval line = subarray(split(line, "\n"), 1) | explode line | parsecsv sepal_length, sepal_width, petal_length, petal_width, species
| eval sepal_length = double(sepal_length), sepal_width = double(sepal_width), petal_length = double(petal_length), petal_width = double(petal_width)
```



## stocks

```
wget url="https://raw.githubusercontent.com/logpresso/dataset/main/stocks.csv" | eval line = subarray(split(line, "\n"), 1) | explode line | parsecsv date, stocks
| eval date = date(date, "yyyyMMdd"), stocks = long(stocks)
| sort date
```


## titanic

```
wget url="https://raw.githubusercontent.com/logpresso/dataset/main/titanic/train.csv" | eval line = subarray(split(line, "\n"), 1) | explode line | parsecsv PassengerId, Survived, Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked
| eval Age=int(Age), Cabin=case(Cabin=="", null, Cabin), Fare=double(Fare), Parch=int(Parch), PassengerId=int(PassengerId), Pclass=int(Pclass),  SibSp=int(SibSp), Survived=int(Survived)
```

```
wget url="https://raw.githubusercontent.com/logpresso/dataset/main/titanic/test.csv" | eval line = subarray(split(line, "\n"), 1) | explode line | parsecsv PassengerId, Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked
| eval Age=int(Age), Cabin=case(Cabin=="", null, Cabin), Fare=double(Fare), Parch=int(Parch), PassengerId=int(PassengerId), Pclass=int(Pclass), SibSp=int(SibSp)
```

```
wget url="https://raw.githubusercontent.com/logpresso/dataset/main/titanic/gender_submission.csv"
| eval line = subarray(split(line, "\n"), 1) | explode line | parsecsv PassengerId, Survived
| eval Survived=int(Survived)
```
