---
title: "np.nan, np.inf, -np.inf 대체/삭제 등 처리"
layout: post
date: 2022-01-27
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Python
- datahandling
category: blog
author: 12#
description:
---
#### 요약 :
데이터에 nan 또는 inf 값이 있을 때 이를 제거(또는 대체)하고 분석하고 싶다면?


```python
import numpy as np
import pandas as pd
```

예시 데이터프레임 


```python
df = pd.DataFrame({'x':[1,2,-3,4,5], 'y':[np.nan,0,0,4,5], 'z':[np.nan,np.inf,-np.inf,1,2]})
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.0</td>
      <td>inf</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3</td>
      <td>0.0</td>
      <td>-inf</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



결측치대체하기


```python
df.fillna(999) # nan만 대체됨
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>999.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.0</td>
      <td>inf</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3</td>
      <td>0.0</td>
      <td>-inf</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.replace([np.inf, -np.inf], 999)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3</td>
      <td>0.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.replace([np.nan, np.inf, -np.inf], 999)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>999.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3</td>
      <td>0.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1 = df.copy().replace([np.inf, -np.inf], np.nan) # inf, -inf를 nan으로 대체
df1.fillna(999, inplace=True) 
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>999.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3</td>
      <td>0.0</td>
      <td>999.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



결측치가 있는 행 제거하기


```python
df.dropna() # nan가 있는 행만 제거됨
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.0</td>
      <td>inf</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-3</td>
      <td>0.0</td>
      <td>-inf</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[np.isfinite(df).all(1)] # nan, inf, -inf 제거
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[~df.isin([np.nan, np.inf, -np.inf]).any(1)] # nan, inf, -inf 제거
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1 = df.copy().replace([np.inf, -np.inf], np.nan) # inf, -inf를 nan으로 대체
df1.dropna(inplace=True) # nan 제거
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 참고

numpy.isnan: NaN일 경우 True  
https://numpy.org/doc/stable/reference/generated/numpy.isnan.html


```python
print(np.isnan(1), np.isnan(np.nan), np.isnan(np.inf), np.isnan(-np.inf))
```

    False True False False
    

numpy.isinf: inf 또는 -inf일 경우 True  
https://numpy.org/doc/stable/reference/generated/numpy.isnan.html


```python
print(np.isinf(1), np.isinf(np.nan), np.isinf(np.inf), np.isinf(-np.inf))
```

    False False True True
    

numpy.isfinite : NaN 또는 Infinity가 아닐 경우 True  
https://numpy.org/doc/stable/reference/generated/numpy.isinf.html


```python
print(np.isfinite(1), np.isfinite(np.nan), np.isfinite(np.inf), np.isfinite(-np.inf))
```

    True False False False
    

numpy.isposinf / numpy.isneginf : 양/음의 무한값(positive/negative infinity)이면 True  
https://numpy.org/doc/stable/reference/generated/numpy.isposinf.html  


```python
print(np.isposinf(1), np.isposinf(np.inf), np.isposinf(-np.inf),  np.isposinf(np.nan))
```

    False True False False
    


```python
print(np.isneginf(1), np.isneginf(np.inf), np.isneginf(-np.inf), np.isneginf(np.nan))
```

    False False True False
    
