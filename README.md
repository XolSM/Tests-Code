# Collection of code developed by me to solve tests while I practice some coding skills: Python, SQL, R

Content:
* [Python](#python)
     - [Final Quiz Answer - Learn Python Basics for Data Analysis](#python-basics)
          - [Question X](#question-x)
          - [Question Y](#question-y)
          - [Question Z](#question-z)
     - [Weekly Python Challenge #27 by Data in Motion LLC](#python-27)
* [MYSQL](#sql)
     - [# MySQL - Weekly SQL Challenge #27 by Data in Motion LLC on LeetCode](#sql-27)

<a id="python"></a>
## Python

<a id="python-basics"></a>
### Final Quiz Answer - Learn Python Basics for Data Analysis
<a id="question-x"></a>
#### Question X:
Consider the following experiment:

A normally-balanced die (with six faces) is thrown 10,000 times. Among these 10,000 throws, 1,000 are taken at random.

We carry out this experiment five times, and we write down m, the average number of times we get the number six out of the 10,000 throws, and n, the average number of times we get the number four in the subsample.

What would be the values of m and n at the end of this experiment?

```{}
import random
nExp = 5 #amount of times required to repeat the experiment
nDiceThrow = 10000
nsubsample = 1000
diceFaces = ["one","two","three","four","five","six"]
mexperiment = [] #list to storage the average of "six" obtained on each experiment
nexperiment = [] #list to storage the average of "four" obtained on each experiment
for ia in range(nExp):
  Xsample = [] #list to storage results for the nDiceThrow
  for ib in range(nDiceThrow):
    Xsample.append(random.choice(diceFaces))
  mcount = Xsample.count("six")
  m = float(mcount / nDiceThrow)
  mexperiment.append(m)
  Xsubsample = random.sample(Xsample, nsubsample)
  ncount = Xsubsample.count("four")
  n = float(ncount / nsubsample)
  nexperiment.append(n)
print(sum(mexperiment)/len(mexperiment))
print(sum(nexperiment)/len(nexperiment))
```
##### Results:
* m = apróx 1/6
* n = apróx 1/6

<a id="question-y"></a>
#### Question Y:
Let's consider two games of chance: 

The next two questions will be based on these two sets.

First, a game that we will call A, which is a simple coin flip with a biased coin (tails with a probability of p=0.49). The player bets one dollar and flips the coin: if they get tails, they win one dollar and recoup their bet, otherwise they lose their bet.
Then, a game that we will call B, which is a game with two biased coins. The first coin gives tails with probability p1 = 0.09 and the second coin gives tails with probability p2 = 0.74. The player can only bet one dollar at a time! However, at each flip, we look at the player's total amount of money to determine which coin to flip: if the amount is a multiple of three, we flip the first coin, otherwise we flip the second coin. As in game A, the player recoups their bet plus an extra dollar if the chosen coin lands on tails, otherwise they lose their bet.
A game is considered won when a player finishes with more money than they started with after playing a large number of rounds (e.g., several hundred). Implement these two games of chance with Python, using the libraries seen earlier, considering that the player starts with a capital of $1,000. 

Which of the following statements is true?

* Game A is a loser while Game B is a winner.
* Both games are winners.
* **Both games are losers.**
* We cannot determine from the information given.

```{}
#Establishing the basic function of the game, coin flip with variable probability (prob)
def flip(prob):
  ran = random.random()
  return 'T' if ran <= prob else 'H'

#Game A
nA = 100000
MoneyA = 1000
for i in range(nA):
  if flip(0.49) == "T":
    MoneyA += 1
  else:
    MoneyA -= 1
if MoneyA > 1000:
  print("Win")
else:
  print("Loss")

#Game B
nB = 100000
MoneyB = 1000
p1=0.09
p2=0.74
for i in range(nB):
  if MoneyB % 3 == 0: #Condition to flip the coin with probability p1 (0.09) if the amount of money on hand is multiple of 3
    pb = p1
  else:               #Otherwise, flip the coin with probability p2 (0.74) if the amount of money on hand is not multiple of 3
    pb = p2
  if flip(pb) == "T": 
    MoneyB += 1
  else:
    MoneyB -= 1
  
if MoneyB > 1000:
  print("Win")
else:
  print("Loss")
```

##### Results:
* Loss
* Loss

<a id="question-z"></a>
#### Question Z:
We will now mix the two games presented in the previous question! Effectively, at each turn, we now flip a coin which is balanced! If you have tails, you play game A, otherwise you play game B.

It is assumed that the player has $1,000 as starting capital.

After playing 1,000,000 games, what is the status of the game, from the player's point of view?

**The game is Won.**

```{}
nCOp = 1000000
MoneyCOp = 1000
pCB1=0.09
pCB2=0.74
pCA3=0.49
for i in range(nCOp):
  flips = [flip(0.5)]
  if flips.count('T') == 0:
    if MoneyCOp % 3 == 0:
      pCOp = pCB1
    else:
      pCOp = pCB2
  else:
    pCOp = pCA3
  if flip(pCOp) == "T":
    MoneyCOp += 1
  else:
    MoneyCOp -= 1
if MoneyCOp > 1000:
  print("Win")
else:
  print("Loss")
```
##### Results:
* Win

<a id="python-27"></a>
### Weekly Python Challenge #27 by Data in Motion LLC

Question
Characters and ASCII Code Dictionary

Write a function that transforms a list of characters into a list of dictionaries, where: The keys are the characters themselves. The values are the ASCII codes of those characters.

Examples to_dict(["a", "b", "c"]) ➞ [{"a": 97}, {"b": 98}, {"c": 99}]
to_dict(["^"]) ➞ [{"^": 94}]
to_dict([]) ➞ []

```{}
import string
def to_dictXSM(input = [""]):
  dictXSM = {}
  for UbicInList in input:
    dictXSM[UbicInList] = ord(UbicInList)
  return print(dictXSM)#Output
```

Test:
```{}
to_dictXSM(["a", "b", "c"])

to_dictXSM(["^"])

to_dictXSM([])
```

##### Results:
* {'a': 97, 'b': 98, 'c': 99}
* {'^': 94}
* {}

<a id="sql"></a>
## MySQL
<a id="sql-27"></a>
### MySQL - Weekly SQL Challenge #27 by Data in Motion LLC on LeetCode

Given the following Tables:

Table: Users
Column Name     | Type    
--------------- | --------
 user_id        | int     
 join_date      | date    
 favorite_brand | varchar 

user_id is the primary key of this table.
This table has the info of the users of an online shopping website where users can sell and buy items.
 

Table: Orders
 Column Name   | Type    
---------------|---------
 order_id      | int     
 order_date    | date    
 item_id       | int     
 buyer_id      | int     
 seller_id     | int     

order_id is the primary key of this table.
item_id is a foreign key to the Items table.
buyer_id and seller_id are foreign keys to the Users table.
 

Table: Items
 Column Name   | Type    
---------------|---------
 item_id       | int     
 item_brand    | varchar 

item_id is the primary key of this table.
 

Write an SQL query to find for each user, the join date and the number of orders they made as a buyer in 2019.
Return the result table in any order.

The query result format is in the following example.
Example 1:
Output: 
 buyer_id  | join_date  | orders_in_2019 
-----------|------------|----------------
 1         | 2018-01-01 | 1              
 2         | 2018-02-09 | 2              
 3         | 2018-01-19 | 0              
 4         | 2018-05-21 | 0              


My answer:
```{}
SELECT 
    Users.user_id as buyer_id,
    Users.join_date,
    Count(order_id) AS orders_in_2019
FROM Users
LEFT JOIN Orders ON Users.user_id = Orders.buyer_id
AND year(order_date) = 2019
GROUP BY Users.user_id
```

##### Results:
* Approved by LeedCode


#####To be continued..😉
