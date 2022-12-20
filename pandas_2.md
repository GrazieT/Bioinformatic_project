## pandas 新增数据列
1. 直接赋值
2. df.apply
3. df.assign
4. 按条件选择分组分别赋值


```python
import numpy as np
import pandas as pd
```

### 读取数据


```python
df = pd.read_table('../name_id.xls', sep = '\t', header = None, names = ['samples', 'subpopulation'])
df.head()
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
      <th>samples</th>
      <th>subpopulation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>110</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>111</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>113</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>117</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>120</td>
      <td>CA</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.set_index('samples', inplace = True)
df.head()
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
      <th>subpopulation</th>
    </tr>
    <tr>
      <th>samples</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>110</th>
      <td>CA</td>
    </tr>
    <tr>
      <th>111</th>
      <td>CA</td>
    </tr>
    <tr>
      <th>113</th>
      <td>CA</td>
    </tr>
    <tr>
      <th>117</th>
      <td>CA</td>
    </tr>
    <tr>
      <th>120</th>
      <td>CA</td>
    </tr>
  </tbody>
</table>
</div>



### 直接赋值


```python
df.loc[:, 'order'] = [int(i) for i in range(1,253)]
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
      <th>subpopulation</th>
      <th>order</th>
    </tr>
    <tr>
      <th>samples</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>110</th>
      <td>CA</td>
      <td>1</td>
    </tr>
    <tr>
      <th>111</th>
      <td>CA</td>
      <td>2</td>
    </tr>
    <tr>
      <th>113</th>
      <td>CA</td>
      <td>3</td>
    </tr>
    <tr>
      <th>117</th>
      <td>CA</td>
      <td>4</td>
    </tr>
    <tr>
      <th>120</th>
      <td>CA</td>
      <td>5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>P81</th>
      <td>WA</td>
      <td>248</td>
    </tr>
    <tr>
      <th>P84</th>
      <td>WA</td>
      <td>249</td>
    </tr>
    <tr>
      <th>P8</th>
      <td>WA</td>
      <td>250</td>
    </tr>
    <tr>
      <th>P14</th>
      <td>OG</td>
      <td>251</td>
    </tr>
    <tr>
      <th>P28</th>
      <td>OG</td>
      <td>252</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 2 columns</p>
</div>



### df.apply方法
* Apply a function along an axis of the DataFrame
* Objects passed to the function are Series objects whose index is either the DataFrame's index(axis=0)
* or the DataFrame's columns(axis = 1)
* 实例：添加一列中文注释：
    1. 如果为CA，则注释为栽培薄皮
    2. 如果为WA，则注释为野生薄皮
    3. 如果为MP，则注释为马泡
    4. 如果为OG，则注释为外群


```python
def add_column(x):
    if x['subpopulation'] == 'CA':
        return "栽培薄皮"
    elif x['subpopulation'] == 'WA':
        return "野生薄皮"
    elif x['subpopulation'] == 'MP':
        return "马泡"
    else:
        return "外群"
df.loc[:, 'un'] = df.apply(add_column, axis = 1)
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
      <th>subpopulation</th>
      <th>order</th>
      <th>un</th>
    </tr>
    <tr>
      <th>samples</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>110</th>
      <td>CA</td>
      <td>1</td>
      <td>栽培薄皮</td>
    </tr>
    <tr>
      <th>111</th>
      <td>CA</td>
      <td>2</td>
      <td>栽培薄皮</td>
    </tr>
    <tr>
      <th>113</th>
      <td>CA</td>
      <td>3</td>
      <td>栽培薄皮</td>
    </tr>
    <tr>
      <th>117</th>
      <td>CA</td>
      <td>4</td>
      <td>栽培薄皮</td>
    </tr>
    <tr>
      <th>120</th>
      <td>CA</td>
      <td>5</td>
      <td>栽培薄皮</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>P81</th>
      <td>WA</td>
      <td>248</td>
      <td>野生薄皮</td>
    </tr>
    <tr>
      <th>P84</th>
      <td>WA</td>
      <td>249</td>
      <td>野生薄皮</td>
    </tr>
    <tr>
      <th>P8</th>
      <td>WA</td>
      <td>250</td>
      <td>野生薄皮</td>
    </tr>
    <tr>
      <th>P14</th>
      <td>OG</td>
      <td>251</td>
      <td>外群</td>
    </tr>
    <tr>
      <th>P28</th>
      <td>OG</td>
      <td>252</td>
      <td>外群</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 3 columns</p>
</div>



#### 查看un的计数
* df['un'].value_counts()


```python
df['un'].value_counts()
```




    栽培薄皮    119
    野生薄皮     95
    马泡       36
    外群        2
    Name: un, dtype: int64



### df.assign方法
* Assign new columns to a Dataframe
* Return a **new object** with **all original columns in addition to new ones**.
* 不会修改Dataframe本身，返回的是一个新的对象


```python
# 可以同时新增多个列
df.assign(
    sort = lambda x : x['order'],
    sort1 = lambda x : x['order'] * 2
)
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
      <th>subpopulation</th>
      <th>order</th>
      <th>un</th>
      <th>sort</th>
      <th>sort1</th>
    </tr>
    <tr>
      <th>samples</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>110</th>
      <td>CA</td>
      <td>1</td>
      <td>栽培薄皮</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>111</th>
      <td>CA</td>
      <td>2</td>
      <td>栽培薄皮</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>113</th>
      <td>CA</td>
      <td>3</td>
      <td>栽培薄皮</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>117</th>
      <td>CA</td>
      <td>4</td>
      <td>栽培薄皮</td>
      <td>4</td>
      <td>8</td>
    </tr>
    <tr>
      <th>120</th>
      <td>CA</td>
      <td>5</td>
      <td>栽培薄皮</td>
      <td>5</td>
      <td>10</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>P81</th>
      <td>WA</td>
      <td>248</td>
      <td>野生薄皮</td>
      <td>248</td>
      <td>496</td>
    </tr>
    <tr>
      <th>P84</th>
      <td>WA</td>
      <td>249</td>
      <td>野生薄皮</td>
      <td>249</td>
      <td>498</td>
    </tr>
    <tr>
      <th>P8</th>
      <td>WA</td>
      <td>250</td>
      <td>野生薄皮</td>
      <td>250</td>
      <td>500</td>
    </tr>
    <tr>
      <th>P14</th>
      <td>OG</td>
      <td>251</td>
      <td>外群</td>
      <td>251</td>
      <td>502</td>
    </tr>
    <tr>
      <th>P28</th>
      <td>OG</td>
      <td>252</td>
      <td>外群</td>
      <td>252</td>
      <td>504</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 5 columns</p>
</div>



### 按条件选择分组分别赋值
* 按条件优先选择数据，然后对这部分数据赋值新列


```python
# 创建一个空列（一种创建新列的方法）
# 用到了broadcast机制
df['priority'] = ''
df.loc[df['order'] <= 30, 'priority'] = "第一组"
df.loc[df['order'] > 30, 'priority'] = "第二组"
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
      <th>subpopulation</th>
      <th>order</th>
      <th>un</th>
      <th>priority</th>
    </tr>
    <tr>
      <th>samples</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>110</th>
      <td>CA</td>
      <td>1</td>
      <td>栽培薄皮</td>
      <td>第一组</td>
    </tr>
    <tr>
      <th>111</th>
      <td>CA</td>
      <td>2</td>
      <td>栽培薄皮</td>
      <td>第一组</td>
    </tr>
    <tr>
      <th>113</th>
      <td>CA</td>
      <td>3</td>
      <td>栽培薄皮</td>
      <td>第一组</td>
    </tr>
    <tr>
      <th>117</th>
      <td>CA</td>
      <td>4</td>
      <td>栽培薄皮</td>
      <td>第一组</td>
    </tr>
    <tr>
      <th>120</th>
      <td>CA</td>
      <td>5</td>
      <td>栽培薄皮</td>
      <td>第一组</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>P81</th>
      <td>WA</td>
      <td>248</td>
      <td>野生薄皮</td>
      <td>第二组</td>
    </tr>
    <tr>
      <th>P84</th>
      <td>WA</td>
      <td>249</td>
      <td>野生薄皮</td>
      <td>第二组</td>
    </tr>
    <tr>
      <th>P8</th>
      <td>WA</td>
      <td>250</td>
      <td>野生薄皮</td>
      <td>第二组</td>
    </tr>
    <tr>
      <th>P14</th>
      <td>OG</td>
      <td>251</td>
      <td>外群</td>
      <td>第二组</td>
    </tr>
    <tr>
      <th>P28</th>
      <td>OG</td>
      <td>252</td>
      <td>外群</td>
      <td>第二组</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 4 columns</p>
</div>




```python
df['priority'].value_counts()
```




    第二组    222
    第一组     30
    Name: priority, dtype: int64


