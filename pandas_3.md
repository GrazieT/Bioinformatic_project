## pandas 数据统计函数
1. 汇总类统计
2. 唯一去重和按值计数
3. 相关系数和方差


```python
import pandas as pd
```


```python
sample = pd.read_table('../name_id.xls', header = None, sep = '\t', names = ['samples', 'subpopulation'])
sample.head()
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
sample.set_index('samples', inplace = True)
sample.head(10)
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
    <tr>
      <th>124</th>
      <td>CA</td>
    </tr>
    <tr>
      <th>128</th>
      <td>CA</td>
    </tr>
    <tr>
      <th>129</th>
      <td>CA</td>
    </tr>
    <tr>
      <th>130</th>
      <td>CA</td>
    </tr>
    <tr>
      <th>142</th>
      <td>CA</td>
    </tr>
  </tbody>
</table>
</div>




```python
sample['order'] = [int(i) for i in range(1,253)]
sample.head(10)
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
      <th>124</th>
      <td>CA</td>
      <td>6</td>
    </tr>
    <tr>
      <th>128</th>
      <td>CA</td>
      <td>7</td>
    </tr>
    <tr>
      <th>129</th>
      <td>CA</td>
      <td>8</td>
    </tr>
    <tr>
      <th>130</th>
      <td>CA</td>
      <td>9</td>
    </tr>
    <tr>
      <th>142</th>
      <td>CA</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
sample = sample.assign(
    sort = sample['order'],
    sort1 = sample['order'] * 2
)
sample
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
      <th>sort</th>
      <th>sort1</th>
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
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>111</th>
      <td>CA</td>
      <td>2</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>113</th>
      <td>CA</td>
      <td>3</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>117</th>
      <td>CA</td>
      <td>4</td>
      <td>4</td>
      <td>8</td>
    </tr>
    <tr>
      <th>120</th>
      <td>CA</td>
      <td>5</td>
      <td>5</td>
      <td>10</td>
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
      <td>248</td>
      <td>496</td>
    </tr>
    <tr>
      <th>P84</th>
      <td>WA</td>
      <td>249</td>
      <td>249</td>
      <td>498</td>
    </tr>
    <tr>
      <th>P8</th>
      <td>WA</td>
      <td>250</td>
      <td>250</td>
      <td>500</td>
    </tr>
    <tr>
      <th>P14</th>
      <td>OG</td>
      <td>251</td>
      <td>251</td>
      <td>502</td>
    </tr>
    <tr>
      <th>P28</th>
      <td>OG</td>
      <td>252</td>
      <td>252</td>
      <td>504</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 4 columns</p>
</div>




```python
sample['priority'] = ''
sample.loc[sample['order'] <= 30, 'priority'] = "first group"
sample.loc[sample['order'] > 30, 'priority'] = 'second group'
sample
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
      <th>sort</th>
      <th>sort1</th>
      <th>priority</th>
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
      <td>1</td>
      <td>2</td>
      <td>first group</td>
    </tr>
    <tr>
      <th>111</th>
      <td>CA</td>
      <td>2</td>
      <td>2</td>
      <td>4</td>
      <td>first group</td>
    </tr>
    <tr>
      <th>113</th>
      <td>CA</td>
      <td>3</td>
      <td>3</td>
      <td>6</td>
      <td>first group</td>
    </tr>
    <tr>
      <th>117</th>
      <td>CA</td>
      <td>4</td>
      <td>4</td>
      <td>8</td>
      <td>first group</td>
    </tr>
    <tr>
      <th>120</th>
      <td>CA</td>
      <td>5</td>
      <td>5</td>
      <td>10</td>
      <td>first group</td>
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
      <td>248</td>
      <td>496</td>
      <td>second group</td>
    </tr>
    <tr>
      <th>P84</th>
      <td>WA</td>
      <td>249</td>
      <td>249</td>
      <td>498</td>
      <td>second group</td>
    </tr>
    <tr>
      <th>P8</th>
      <td>WA</td>
      <td>250</td>
      <td>250</td>
      <td>500</td>
      <td>second group</td>
    </tr>
    <tr>
      <th>P14</th>
      <td>OG</td>
      <td>251</td>
      <td>251</td>
      <td>502</td>
      <td>second group</td>
    </tr>
    <tr>
      <th>P28</th>
      <td>OG</td>
      <td>252</td>
      <td>252</td>
      <td>504</td>
      <td>second group</td>
    </tr>
  </tbody>
</table>
<p>252 rows × 5 columns</p>
</div>



### 汇总类统计


```python
# 一次提取所有数字列的统计结果
sample.describe()
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
      <th>order</th>
      <th>sort</th>
      <th>sort1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>252.000000</td>
      <td>252.000000</td>
      <td>252.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>126.500000</td>
      <td>126.500000</td>
      <td>253.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>72.890329</td>
      <td>72.890329</td>
      <td>145.780657</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>63.750000</td>
      <td>63.750000</td>
      <td>127.500000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>126.500000</td>
      <td>126.500000</td>
      <td>253.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>189.250000</td>
      <td>189.250000</td>
      <td>378.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>252.000000</td>
      <td>252.000000</td>
      <td>504.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看单个列
display(sample['order'].mean())
display(sample['order'].max())
display(sample['order'].min())
```


    126.5



    252



    1


### 唯一去重和按值计数

#### 唯一性去重


```python
sample['priority'].unique()
```




    array(['first group', 'second group'], dtype=object)



#### 按值计数


```python
sample['priority'].value_counts()
```




    second group    222
    first group      30
    Name: priority, dtype: int64



### 相关系数和协方差
* 协方差：衡量同向反向程度， 如果协方差为正， 说明X、Y同向变化， 协方差越大说明同向程度越高； 如果协方差为负， 说明X、Y反向运动， 想方差越小说明反向程度越高
* 相关系数： 衡量相似度程度， 当他们的相关系数为1时， 说明两个变量变化时的正向相似度最大， 当相关系数为 -1 时， 说明两个变量变化的反向相似度最大


```python
# 协方差
sample.cov()
```

    /var/folders/9_/zjqpf4jd0310k16rbpg_hczw0000gn/T/ipykernel_48691/1778967562.py:2: FutureWarning: The default value of numeric_only in DataFrame.cov is deprecated. In a future version, it will default to False. Select only valid columns or specify the value of numeric_only to silence this warning.
      sample.cov()





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
      <th>order</th>
      <th>sort</th>
      <th>sort1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>order</th>
      <td>5313.0</td>
      <td>5313.0</td>
      <td>10626.0</td>
    </tr>
    <tr>
      <th>sort</th>
      <td>5313.0</td>
      <td>5313.0</td>
      <td>10626.0</td>
    </tr>
    <tr>
      <th>sort1</th>
      <td>10626.0</td>
      <td>10626.0</td>
      <td>21252.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 相关系数
sample.corr()
```

    /var/folders/9_/zjqpf4jd0310k16rbpg_hczw0000gn/T/ipykernel_48691/3606128338.py:2: FutureWarning: The default value of numeric_only in DataFrame.corr is deprecated. In a future version, it will default to False. Select only valid columns or specify the value of numeric_only to silence this warning.
      sample.corr()





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
      <th>order</th>
      <th>sort</th>
      <th>sort1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>order</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>sort</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>sort1</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看单个
display(sample['order'].cov(sample['sort']))
display(sample['order'].corr(sample['sort1']))
display(sample['order'].corr(sample['sort1'] - sample['sort']))
```


    5313.0



    1.0



    1.0


## pandas 缺失值的处理
* pandas使用以下函数处理缺失值：
    * isnull 和 notnull ： 检查是否是空值， 可用于df和series
    * dropna ： 丢弃、删除缺失值
        * axis ： 删除行还是列， 0 for index ，1 for columns， default is 0
        * how ： 如果等于any则任何值为空都删除， 如果等于all则所有值为空才删除
        * inplace ： 如果为True则修改当前的df， False则返回新的df
    * fillna ：填充空值
        * value ： 要填充的值， 可以是单个值， 也可以是字典（key是列名，value是值）
        * method ： 等于 ffill 使用前一个不为空的值来填充， 等于 bfill 使用后一个不为空的值来填充
        * axis ： 按行还是列填充
        * inplace ： 返回的对象

### 读取excel


```python
import openpyxl
df = pd.read_excel('../pd_test.xlsx', skiprows = 0)
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
      <th>姓名</th>
      <th>科目</th>
      <th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>小明</td>
      <td>语文</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小王</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>数学</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>小刚</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>英语</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### 检查空值


```python
df.isnull()
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
      <th>姓名</th>
      <th>科目</th>
      <th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['分数'].isnull()
```




    0      True
    1     False
    2     False
    3      True
    4     False
    5      True
    6     False
    7      True
    8     False
    9     False
    10     True
    Name: 分数, dtype: bool




```python
# 筛选没有空分数的所有行
df.loc[df['分数'].notnull() , :]
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
      <th>姓名</th>
      <th>科目</th>
      <th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小王</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>小刚</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
  </tbody>
</table>
</div>



### 删除掉全是空值的列


```python
df.dropna(axis = 'columns', how = 'all', inplace = True)
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
      <th>姓名</th>
      <th>科目</th>
      <th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>小明</td>
      <td>语文</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小王</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>数学</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>小刚</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>英语</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### 删除掉全是空值的行


```python
df.dropna(axis = 'index', how = 'all', inplace = True)
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
      <th>姓名</th>
      <th>科目</th>
      <th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>小明</td>
      <td>语文</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小王</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>数学</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>小刚</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>英语</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### 将分数列的空值填充为0


```python
df['分数'].fillna(0, inplace = True)
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
      <th>姓名</th>
      <th>科目</th>
      <th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>小明</td>
      <td>语文</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小王</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>数学</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>小刚</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>英语</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 另一种方法
df.fillna({'分数' : 0}, inplace = True)
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
      <th>姓名</th>
      <th>科目</th>
      <th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>小明</td>
      <td>语文</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小王</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>数学</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>小刚</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>英语</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



### 对姓名列的缺失值进行填充


```python
df['姓名'].fillna(method = 'ffill', inplace = True)
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
      <th>姓名</th>
      <th>科目</th>
      <th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>小明</td>
      <td>语文</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>小明</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>小明</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>小王</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>小王</td>
      <td>数学</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>小王</td>
      <td>英语</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>小刚</td>
      <td>语文</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>小刚</td>
      <td>数学</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>小刚</td>
      <td>英语</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



### 将清洗好的excel保存


```python
df.to_excel('../pd_test_clean.xlsx', index = False)
```
