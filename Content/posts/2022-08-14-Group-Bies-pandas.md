---
title: Group by pandas operations From Zero to Hero
date: 2022-08-14 8:05
description: steps to make easy group by operations from easy operations to advanced ones.
tags: Python, Basics
path: Group bies
author: Mohamed Fares Ben Ayed
---

# Group by pandas operations: From Zero to Hero

## What is aggregation?

One of the important Tools in data science is to know how to aggregate data, Aggregation techniques enable the programmer (or the data scientist) to understand more about the data he's working on.

But what is aggregation exactly? Aggregation is to group the data observations into distinct groups (or categories) and then we can apply some statistical functions on those groups like mean, median, standard deviation, sum, product, count, minimum, maximum and many other cool functions.

After reading this post, we'll be able to work with any kind of dataset and apply complex groupby operations. In this post we will work on the pokemon data (The anime of pokemon and its video games). we don't need to worry! we will explain each detail of this data before moving to the code.

To download the dataset, click this [link](https://gist.githubusercontent.com/armgilles/194bcff35001e7eb53a2a8b441e8b2c6/raw/92200bc0a673d5ce2110aaad4544ed6c4010f687/pokemon.csv). it is a link from github that contains the raw data of the pokemon dataset. we can notice that the format of data is similar to the format of a csv file

We can read the dataset directly from the provided github link. Here is our starting block of code:

```Python
import pandas as pd
path='https://gist.githubusercontent.com/armgilles/194bcff35001e7eb53a2a8b441e8b2c6/raw/92200bc0a673d5ce2110aaad4544ed6c4010f687/pokemon.csv'
pokemon_data = pd.read_csv(path, index_col = '#')
```

This our post summary:

1. [Dataset review and understanding.](#dataset-review-and-understanding)
2. [Code steps](#code-steps)
3. [Step 1](#step-1)
4. [Step 2](#step-2)
5. [Step 3](#step-3)
6. [Step 4](#step-4)

## Dataset review and understanding

![Description of a Pokemon](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cn1ll8f44rugv14zaynd.png)

Pokemon is an anime which the main character always wants to collect pokemon monsters and we need to help him to know more about those pokemons.

So, our data is definitely about pokemon monsters, each observation of pokemon data represents a pokemon(a certain monster).

Every pokemon has a set of attributes like Attack, Defense, HP and Monster Type.

Our dataset contains a set of 11 columns (excluding the name of the pokemon):

- `Type 1` : the type of a pokemon, the pokemon can have type like Grass, Fire or any other attribute.
- `Type 2` : the same as the first attribute, but with different types.
- `Total` : the total sum of the following numerical attributes.
- `Attack` : this column describes the attack points of a monster.
- `Defense` : this column describes the defense points of a monster.
- `HP` : this column describes the health points of a monster.
- `Sp. ATK` : this column describes the special attack points of a monster.
- `Sp. DEF` : this column describes the special defense points of a monster.
- `Speed` : this column describes the speed points of a monster.
- `Generation` : this column describes the generation category, it is ranked from 1 to 6.
- `Legendary` : this column describes whether the monster has a legendary class or not, it is represented by boolean a value (True or False).

Now, after we read the dataset, we need to move on the next steps of learning groupby operations. But before that we need to make a few lines of codes.

```Python
del pokemon_data['Name']
```

The code above deleted the `Name` column, because we don't need a string information in our data. groupby operations need just categorical or numerical information.

## Code steps

### From zero to hero.

In this section, we will introduce our learning steps of groupby operations. each step will state a statistical question, and we will show the code that will provide the output to that question.

this is our final working dataset:
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/msmz5zy812e2efvb9er4.png)

#### Step 1

##### Apply a groupby operation with a mean function.

- Question : what is the mean `Total` attribute for each pokemon `Generation` attribute?

- Answer : First, you need to group the data into a `Generation` group, and then apply the mean on the `Total`.

- Code:

```Python
pokemon_data[['Total', 'Generation']].groupby('Generation').mean()
```

Output:

| Generation | Total      |
| ---------- | ---------- |
| 1          | 426.813253 |
| 2          | 418.283019 |
| 3          | 436.225000 |
| 4          | 459.016529 |
| 5          | 434.987879 |
| 6          | 436.378049 |

This can be done with the `sum()` function, the `min()` functions and many other statistical functions.

Try this block of code, to try out different aggregate functions:

```Python
pokemon_data[['Total', 'Generation']].groupby('Generation').size() #aggregate by counting the values
pokemon_data[['Total', 'Generation']].groupby('Generation').min() #aggregate by minimum
pokemon_data[['Total', 'Generation']].groupby('Generation').max() #aggregate by maximum
pokemon_data[['Total', 'Generation']].groupby('Generation').std() #aggregate by standard deviation
pokemon_data[['Total', 'Generation']].groupby('Generation').sum() #aggregate by sum
pokemon_data[['Total', 'Generation']].groupby('Generation').prod() #aggregate by production
```

#### Step 2

##### Multiple aggregate functions in a single groupby

- Question : Now, what is the mean and standard deviation of `Speed` attribute for each generation ?

- Answer : we can aggregate multiple functions in a single output using the `agg()` function.

- Code : There are 2 versions of code that can result the same output, the second one is a simplified version :

1. Code 1 :

```Python
pokemon_data.groupby("Generation").agg(
   average_speed = pd.NamedAgg("Speed","mean"), # here we apply the mean
   std_speed = pd.NamedAgg("Speed", "std"), # here we apply the standard deviation
)
```

2. Code 2 :

```Python
pokemon_data.groupby("Generation").agg(
average_speed=("Speed","mean"), # applying the mean
std_speed = ("Speed", "std"), # applying the standard deviation
)
```

- Output :

| Generation | average_speed | std_speed |
| ---------- | ------------- | --------- |
| 1          | 72.584337     | 29.675857 |
| 2          | 61.811321     | 27.263132 |
| 3          | 66.925000     | 31.331972 |
| 4          | 71.338843     | 28.475005 |
| 5          | 68.078788     | 28.726632 |
| 6          | 66.439024     | 25.691954 |

#### Step 3:

##### Group by multiple columns.

- Question : what is the maximum `Attack` attribute for each `Generation` attribute? and we want to know which `Legendary` attribute has the maximum `Attack` for each `Generation`.

- Answer : we can do that by goruping by `Generation` and `Legendary` at the same time.

- Code :

```Python
pokemon_data.groupby(['Generation', 'Legendary']).agg(
maximum_attack = ('Attack', 'max')
)
```

- Output :

<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">Generation</th>
    <th class="tg-0pky">Legendary</th>
    <th class="tg-0pky">maximum_attack</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky" rowspan="2">1</td>
    <td class="tg-0pky">True</td>
    <td class="tg-0pky">155</td>
  </tr>
  <tr>
    <td class="tg-0pky">False</td>
    <td class="tg-0pky">190</td>
  </tr>
  <tr>
    <td class="tg-0pky" rowspan="2">2</td>
    <td class="tg-0pky">True</td>
    <td class="tg-0pky">185</td>
  </tr>
  <tr>
    <td class="tg-0pky">False</td>
    <td class="tg-0pky">130</td>
  </tr>
  <tr>
    <td class="tg-0pky" rowspan="2">3</td>
    <td class="tg-0pky">True</td>
    <td class="tg-0pky">165</td>
  </tr>
  <tr>
    <td class="tg-0pky">False</td>
    <td class="tg-0pky">180</td>
  </tr>
  <tr>
    <td class="tg-0pky" rowspan="2">4</td>
    <td class="tg-0pky">True</td>
    <td class="tg-0pky">170</td>
  </tr>
  <tr>
    <td class="tg-0pky">False</td>
    <td class="tg-0pky">160</td>
  </tr>
  <tr>
    <td class="tg-0pky" rowspan="2">5</td>
    <td class="tg-0pky">True</td>
    <td class="tg-0pky">147</td>
  </tr>
  <tr>
    <td class="tg-0pky">False</td>
    <td class="tg-0pky">170</td>
  </tr>
  <tr>
    <td class="tg-0pky" rowspan="2">6</td>
    <td class="tg-0pky">True</td>
    <td class="tg-0pky">150</td>
  </tr>
  <tr>
    <td class="tg-0pky">False</td>
    <td class="tg-0pky">160</td>
  </tr>
</tbody>
</table>

#### Step 4:

##### Sorting group results. (Multiple column case)

- Question : What are the types (`Type 1` to be specific) of pokemon that have the maximum `Attack` attributes for each `Generation` column? the results need to be sorted, so that the maximum value for each Generation and type will be spotted easily.

- Answer : Code and output will explain.

- Code :

```Python
pokemon_data.groupby(['Generation', 'Legendary']).agg(
maximum_attack = ('Attack', 'max')
).sort_values(by = 'maximum_attack', ascending = False)
```

- Output : The output is specified with `Generation` 1 attribute.

<table class="tg">
<thead>
  <tr>
    <td class="tg-0lax" rowspan="15">1</td>
    <td class="tg-lqy6"><span style="font-weight:normal">Psychic</span></td>
    <td class="tg-mwxe">190</td>
  </tr>
  <tr>
    <td class="tg-p3ql"><span style="font-weight:normal">Bug</span></td>
    <td class="tg-p3ql">155</td>
  </tr>
  <tr>
    <td class="tg-mwxe"><span style="font-weight:normal">Water</span></td>
    <td class="tg-mwxe">155</td>
  </tr>
  <tr>
    <td class="tg-p3ql"><span style="font-weight:normal">Rock</span></td>
    <td class="tg-p3ql">135</td>
  </tr>
  <tr>
    <td class="tg-mwxe"><span style="font-weight:normal">Dragon</span></td>
    <td class="tg-mwxe">134</td>
  </tr>
  <tr>
    <td class="tg-p3ql"><span style="font-weight:normal">Fighting</span></td>
    <td class="tg-p3ql">130</td>
  </tr>
  <tr>
    <td class="tg-mwxe"><span style="font-weight:normal">Fire</span></td>
    <td class="tg-mwxe">130</td>
  </tr>
  <tr>
    <td class="tg-p3ql"><span style="font-weight:normal">Ground</span></td>
    <td class="tg-p3ql">130</td>
  </tr>
  <tr>
    <td class="tg-mwxe"><span style="font-weight:normal">Normal</span></td>
    <td class="tg-mwxe">125</td>
  </tr>
  <tr>
    <td class="tg-p3ql"><span style="font-weight:normal">Grass</span></td>
    <td class="tg-p3ql">105</td>
  </tr>
  <tr>
    <td class="tg-mwxe"><span style="font-weight:normal">Poison</span></td>
    <td class="tg-mwxe">105</td>
  </tr>
  <tr>
    <td class="tg-p3ql"><span style="font-weight:normal">Electric</span></td>
    <td class="tg-p3ql">90</td>
  </tr>
  <tr>
    <td class="tg-mwxe"><span style="font-weight:normal">Ice</span></td>
    <td class="tg-mwxe">85</td>
  </tr>
  <tr>
    <td class="tg-p3ql"><span style="font-weight:normal">Fairy</span></td>
    <td class="tg-p3ql">70</td>
  </tr>
  <tr>
    <td class="tg-mwxe"><span style="font-weight:normal">Ghost</span></td>
    <td class="tg-mwxe">65</td>
  </tr>
</thead>
</table>

#### Step 5:

##### use groupbies with filtering:

This step won't be in question/Answer format.
We can filter our data by `Type 1` for example:

```Python
pokemon_data[pokemon_data['Type 1'] == 'Water'].head()
# or
pokemon_data.loc[ pokemon_data['Type 1'] == 'Water' , ['Attack']]
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zwe5z68w8678q906w0o1.png)

Now we need to use a grouby operation with a filter:

```Python
grouped = pokemon_data.groupby('Type 1')
grouped.filter(lambda x: x['Attack'].mean() > 100)
```

This code displays only the **Dragon** type, because the mean attack of all dragon pokemons is above 100.
