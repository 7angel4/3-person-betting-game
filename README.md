# 3-person-betting-game

<h2>Game description</h2>

A betting game involves 3 players, that start the game with amounts of money $ $x, $y, $z $ (all > 0) respectively. At each round $n \in \mathbb{N}$ of the game, one player (the <i>giver</i>) is chosen uniformly at random to give some money to one of the other players (the <i>receiver</i>) chosen uniformly at random (independent of previous rounds). If these two chosen players had $\$V$ and $\$W$ at the beginning of the round, then the giver must give the receiver $ \min \{ \$V, \$W \} $, and the round ends.

The first player to reach $ \$0 $ in this game is called the <i>loser</i>. After a loser has been determined the remaining two players continue until one of those two players has all the money. The player with all of the money at the end is called the <i>winner</i>.

Let the amounts of money at time $n$ (i.e. after $n$ rounds) of the 3 players be $X_n, Y_n, Z_n$ respectively (so $X_0 = x, Y_0 = y, Z_0 = z$). Let $T_1 = \inf \{n >= 1: \min \{X_n, Y_n, Z_n \} = 0 \} $ and $T_2 = \inf \{n >= 1: \max \{X_n, Y_n, Z_n \} = x+y+z \} $.


<h2>Goal</h2>

Finding the probability that a given player is the winner is simple. For example, the probability that Player 1 wins is just $\frac {x} {x+y+z}$.

However, finding the probability that a given player is the loser is much more difficult. The first-step analysis could involve many more intermediate states and generate many equations.

Thus, this Python program serves to find the exact probability (as a fraction) that Player 1 is the loser of the game, for any initial state $(x, y, z)$.

<h2>Main files</h2>

`LoserAnalysis.ipynb`: The main notebook which includes
* the `LoserAnalysis` class: represents the first step analysis of the hitting probability from the provided initial state to a state where loser = Player 1.
* the `exportStateProbs` function: generates the hitting probabilities from all initial states within a certain range, and exports the information to a CSV file with columns (Initial state, P(Loser = Player 1)).

`BettingGameSimulation.ipynb`: An additional notebook featuring the `simGame` function, which simulates the game for a specified number of times, and outputs a summary of the game statistics.<br>
This file could be used to generate numerical approximations to $P(\text{Loser} = \text{Player 1})$, and as a sanity check for the exact solutions generated in `LoserAnalysis.ipynb`.

`578Equations.txt`: Sample text file illustrating what is created by the `exportEqns` method in the `LoserAnalysis` class.<br>

`Player1LoseProbs_1to5.csv`: Sample CSV file illustrating what is created by the `exportStateProbs` function.

<h2>Running the program</h2>

a) From Jupyter Notebook: 

Simply click `Kernel > Restart & Run All` to run all cells.<br>
Then append any necessary function calls to attain the desired hitting probability.

b) From Terminal:

1. Run `jupyter nbconvert --execute LoserAnalysis --to python`.<br>
This converts the notebook `LoserAnalysis.ipynb` to a Python file, `LoserAnalysis.py`.
2. Open the file and add in any necessary function calls.<br>
Alternatively, run `nano LoserAnalysis.py` to edit the file and append any necessary function calls.
3. Run `python LoserAnalysis.py` to execute the program.<br>
You may wish to run the specific command for your Python version, e.g. `python3.10 LoserAnalysis.py`.
