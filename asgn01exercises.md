# ASGN 01

This assignment covers the basics of writing code in Jupyternote books, loading and saving data, and then working with the basic python structures: strings and lists. You'll also write some functions. The idea is to get familiarity with writing code and thinking and planning out solutions programmatically.

My goal is for everyone to get 100% on this assignment. If you submit the assignment before the second week of class starts, we will give you feedback so that you can revise your solutions and improve your grade. 

I would suggesting opening a tab in your browser to chapter 1.7 of our [textbook](ledatascifi.github.io) and this [explainer](https://nbviewer.org/github/jakevdp/WhirlwindTourOfPython/blob/master/06-Built-in-Data-Structures.ipynb). 

Remember,
1. There are usually MANY ways to achieve things programatically. 
2. You can use external resources to try to figure out things, like saving CSV files. Google is your friend!
3. **You must NOT work with other students on this assignment.** The goal of this assignment is to learn how to find resources (Google, Stackoverflow, ledatascifi.github.io) so that you can solve problems. If you can't figure something out, email me and your TA (CC us both).

## Q1. The next cell is Markdown, but it should be python. 

Convert it, then execute it.


```python
for i in range(4,10): 
    print(i)
```

    4
    5
    6
    7
    8
    9


## Q2 Loading data. 

There is a simple csv file in the data subfolder of the repo. Load it and print the first 5 rows. 


```python
import pandas as pd
df = pd.read_csv('data/wordle.csv')
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
      <th>whole_word</th>
      <th>pos1</th>
      <th>pos2</th>
      <th>pos3</th>
      <th>pos4</th>
      <th>pos5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>cigar</td>
      <td>c</td>
      <td>i</td>
      <td>g</td>
      <td>a</td>
      <td>r</td>
    </tr>
    <tr>
      <th>1</th>
      <td>rebut</td>
      <td>r</td>
      <td>e</td>
      <td>b</td>
      <td>u</td>
      <td>t</td>
    </tr>
    <tr>
      <th>2</th>
      <td>sissy</td>
      <td>s</td>
      <td>i</td>
      <td>s</td>
      <td>s</td>
      <td>y</td>
    </tr>
    <tr>
      <th>3</th>
      <td>humph</td>
      <td>h</td>
      <td>u</td>
      <td>m</td>
      <td>p</td>
      <td>h</td>
    </tr>
    <tr>
      <th>4</th>
      <td>awake</td>
      <td>a</td>
      <td>w</td>
      <td>a</td>
      <td>k</td>
      <td>e</td>
    </tr>
  </tbody>
</table>
</div>



## Q3. Saving data.

Save this to a csv file in this folder, and call it "temp.csv". The file should be six lines long.

You can either load this list into a pandas dataframe and use pandas to save it, or else Google "python save list of lists to CSV" and look for a good stackoverflow answer.


```python
an_intermediate_dataset = [['team','opinion'],
                          ['eagles','good'],
                          ['cowboys','trash'],
                          ['giants','double trash'],
                          ['patriots','most trash'],
                          ['lions','who cares-super irrelevant']]
```


```python
df2 = pd.DataFrame(an_intermediate_dataset)
df2.to_csv('temp.csv')
```

## Q4. Slicing and working with lists. What is the...
...sum of the last 5 elements of `list(range(0,100,3))`?


```python
mylist = list(range(0,100,3))
print(sum(mylist[-5:]))
```

    465


## Q5. One more list question. What is the...
...sum of the elements in odd numbered **positions** (where the **index** is odd, not necessarily the content of the element) of  `list(range(0,100,3))`? Remember: The first element in a list is accessed by `list[0]` and the second element in a list is accessed by `list[1]`. So I want you to add the second element, the fourth element, the sixth element, and so on. 


```python
mylist = list(range(0,100,3))

print(sum(mylist[1::2]))

```

    867


## Q6. Function #1 - Working with strings
Write a function that takes a string as an argument and returns the number of capital letters in the string.

Hint: You'll probably use a "for-loop" and an "if-statement".


```python
def count_capitals(inString):
    counter = 0
    for i in inString:
        if i.isupper():
            counter += 1
    return counter

print(count_capitals('Go Tigers!')) # leave this, it's a test unit
print(count_capitals('Hail to the Victors Valiant!')) # leave this, it's a test unit
print(count_capitals("LET'S GO DEVILS!")) # leave this, it's a test unit
```

    2
    3
    12


## Q7. Function #2 - for loops and if-statements

Write a function that takes two sequences, `seq1` and `seq2`, as arguments and returns the number of distinct elements in both. By "sequence" we mean a list, a tuple or a string.

1. **Do not count duplicates!** For example: "ABC" and "BBC" would return 2 ("B" and "C" are in each).
2. And we are comparing **elements**, not letters per se. The first element in the last test below is "j" for the left sequence. For the right sequence, which is a list, the first element is "jet", NOT "j". 

Hint: You'll probably use a "for-loop" and an "if-statement".


```python
def sequence_overlap_count(seq1,seq2):
    counter = 0
    
    for i in list(set(seq1)):
        for j in list(set(seq2)):
            if i == j:
                counter +=1
    return counter

print(sequence_overlap_count((1,2,3),[1,2,3])) # leave this, it's a test unit. Answer = 3
print(sequence_overlap_count('hey there','batter up')) # leave this, it's a test unit. Answer = 4
print(sequence_overlap_count('j',['jet','sweep'])) # leave this, it's a test unit. Answer = 0.

```

    3
    4
    0


## Q8. Function #3
Write a function that counts how many of the pairs have two even numbers.

Hint: You'll probably use a "for-loop" and an "if-statement".


```python
def both_even(list_of_pairs):
    counter = 0
    for i in list_of_pairs:
        if (i[0]%2 ==0) and (i[1]%2==0):
            counter +=1
    return counter

pairs = ((2, 5), (4, 2), (9, 8), (12, 10)) # leave this, it's a test unit
both_even(pairs) # leave this, it's a test unit
```




    2



## Q9. Function #4

Given a list, return the sublist where each element is divisible by 3. 

Hint: You'll probably use a "for-loop" and an "if-statement".


```python
def mod_3_sublist(inList):
    newList = []
    for i in inList:
        if i%3 == 0:
            newList.append(i)
    return newList
    
practice = list(range(1, 100, 7))
mod_3_sublist(practice) # leave this, it's a test unit
```




    [15, 36, 57, 78, 99]



--- 
## Optional advanced problems 

These aren't for credit but offer you ways to practice your programming skills. 

If you attempt them, so **below this cell** to leave your answers above clean. 

### Supercharging your solutions

Each of the above 4 functions can be written in a **single** line of code: `return <your answer here>`

Doing so isn't necessary, but it might help you think about the problems differently and will expose you to another powerful python construct. 

HINT: It involves collapsing your for loops, but the code you've written probably won't need to change much. 

### The WORDLE challenge

The data we loaded in Q2 above is the list of possible answers to WORDLE, a game that suddenly got really popular in the winter of 2022. [If you don't know it, go here to play it (takes < 3 minutes) to see whats going on.](https://www.powerlanguage.co.uk/wordle/)

**To beat all your friends playing the game, here are some things you can try to figure out.** You can try any of them in any order. 
1. Entree challenge: Tell me how many times each letter appears in each spot (e.g. how many times is an "e" in the last letter of a word.
1. Main course: Tell me how many total times each letter appears in the list of words. 
1. Dessert: Tell me what fraction of words each letter appears in. Hint: "A" appears in 39.2% of the words. 
1. Dessert 2: What's the 10 most common two-letter sequence to start the words?
1. Dessert 3: What's the 10 most common two-letter sequence to end the words?
1. Kilimanjaro challenge: **Describe (but don't attempt!)** how you would approach solving for an optimal first word. It's worth thinking about what should be the criteria for an "optimal guess"?
1. Everest challenge: Try to implement your approach to get the optimal first word. 
    
[I made a discussion post for the Wordle challange. Feel free to discuss it there with your classmates. You can work collaboratively to solve the questions if you so choose.](https://github.com/orgs/LeDataSciFi/teams/classmates-2022/discussions/1)
