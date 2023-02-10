# Collection of code developed by me to solve tests while I practice some coding skills: Python, SQL, R

Content:
* [Final Quiz Answer - Learn Python Basics for Data Analysis](#python-basics)
     - [Question X](#question-x)
     - [Question Y](#question-x)

<a id="python-basics"></a>
## Final Quiz Answer - Learn Python Basics for Data Analysis
<a id="question-x"></a>
### Question X:
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

<a id="question-y"></a>
### Question Y:
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
print(MoneyA)

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
print(MoneyB)
```
