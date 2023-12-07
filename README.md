# 3-person-betting-game

<h2>Game description</h2>

A betting game involves 3 players, that start the game with amounts of money $x, $y, $z (all > 0) respectively. 

Let the fortunes at time $n$ (i.e. after $n$ rounds) of the 3 players be $X_n, Y_n, Z_n$ respectively (so $X_0 = x, Y_0 = y, Z_0 = z$), and model $(X_n, Y_n, Z_n)$ as a Markov chain.

At each round of the game:

* **Game 1**: One player (the <i>giver</i>) is chosen uniformly at random to give some money to one of the other players (the <i>receiver</i>) chosen uniformly at random (independent of previous rounds).<br> 
If these two chosen players had $V and $W at the beginning of the round, then the giver must give the receiver $ $\min (V, W)$.
* **Game 2**: one player is chosen uniformly at random as the receiver. All other players give $ $\min (X, Y, Z)$ to the receiver.

And the round ends.

The first player to reach $0 in this game is called the <i>loser</i>. 
* Game 2: If two players are eliminated at the same time, then we toss a fair coin to determine who is the loser.

After a loser has been determined the remaining two players continue until one of those two players has all the money. The player with all of the money at the end is called the <i>winner</i>.

Given initial state $(x, y, z)$, denote: 
* $L_{(x,y,z)}: probability that player 1 loses
* W_{(x,y,z)}: probability that player 1 wins.

<h2>Problem</h2>

Finding the probability that a given player wins is simple. For example, the probability that Player 1 wins is just $\frac {x} {x+y+z}$.

However, finding the probability that a given player is the loser is much more difficult. The first-step analysis could involve many more intermediate states and generate many equations, making the analysis intractable to calculate by hand.

This Python program does exactly this -- it finds the exact probability (as a fraction) that Player 1 is the loser of the game, for any initial state $(x, y, z)$.

<h2>Repo structure<h2>

<code>.<br>
|-- loser-analysis.ipynb<br>
|-- simulation.ipynb<br>
|-- visualiser.ipynb<br>
|-- game1_two_players<br>
|   |-- game1_global.ipynb<br>
|   |-- game1_demo.ipynb<br>
|   |-- game1_loser_analysis.ipynb<br>
|   |-- game1_hitting_probs_generator.ipynb<br>
|   |-- game1_better_giving_1.ipynb<br>
|   |-- game1_memoisation.ipynb<br>
|   |-- game1_visualisation.ipynb<br>
|   |-- data<br>
|   |   |-- game1_demo_(5,7,8)_equations.txt<br>
|   |   |-- game1_demo_probs_1-10.csv<br>
|   |   |-- game1_exact_hitting_probs.csv<br>
|   |   |-- game1_float_hitting_probs.csv<br>
|   |   |-- game1_better_giving_1_stricter_1-100.csv<br>
|   |   |-- ...<br>
|   |<br>
|   |-- visualisation<br>
|   |   |-- game1_hitting_probs (x = 1-300, y = 100, z = 200, t = 30, varyX).png<br>
|   |   |-- game1_hitting_probs (x = 1-300, y = 100, z = 200, t = 30, varyX_memoised).png<br>
|   |   |-- game1_fixed_sum_N=2000_t=30.png<br>
|<br>
|-- game2_three_players<br>
|   |-- ...<br>
</code>

... `./game2_three_players` follow the same structure as `game1_two_players`.

<h2>Programs</h2>

`loser_analysis.ipynb`:
The main `LoserAnalysis` class represents the first-step analysis, given an initial state.

| Function/method | Functionality | Demo/sample results | Notes |
| --- | --- | --- | --- |
| `getHittingProb` (`LoserAnalysis`) | Calculate the exact $L_{(x,y,z)}$ in fraction form | `demo_probs_1-10.csv` | Also allows to approximate $L_{(x,y,z)}$, using memoisation + enumeration of all possible games up to a fixed number of rounds (faster method) |
`getEquations`, `exportEqns` (`LoserAnalysis`) | Generate and export the $L_{(x,y,z)}$ equations | `demo_(5,7,8)_equations.txt` |
| `exportStateProbs` | Generate and export the $L_{(x,y,z)}$'s from all initial states within a certain range | `game*_exact_hitting_probs.csv` | CSV with format: (Initial state, $L_{(x,y,z)}$) |


`simulation.ipynb`:
Provides numerical approximation. Used as a sanity check of the first-step analyses' results.

Main functions:
* `playGame`: Simulates one game
* `playGames`: Simulates multiple games

`visualiser.ipynb`:
| Function | Description | x-axis | y-axis | Sample |
| --- | --- | --- | --- | --- |
| `plotXforFixedYZ` | Plots $L_{(x,y,z)}$ for varying x within a range, fixed y and z | x | $L_{(x,y,z)}$ | `game*_hitting_probs (x = 1-1000, y = 100, z = 200, t = 10, varyX_memoised).png` | 
| `plotFixedSum` | Visualises $L_{(x,y,z)}$'s for fixed sum $x+y+z = N$ | y | z | `game*_fixed_sum_N=2000_t=30.png` |


<h2>Running the programs</h2>

a) From <b>Jupyter Notebook</b>: 

Simply click `Kernel > Restart & Run All` to run all cells.<br>
Or, run the `%run` and `import` cells at the top of the program, then append any necessary function calls to attain the desired effect.

b) From <b>Terminal</b>:

1. Run `jupyter nbconvert --execute <notebook_name> --to python`.<br>
This converts the specified notebook to a Python file, `<notebook_name>.py`.
2. Open the file and add in any necessary function calls.<br>
Alternatively, run `nano <notebook_name>.py` to edit the file and append any necessary function calls.
3. Run `python <notebook_name>.py` to execute the program.<br>
You may wish to run the specific command for your Python version, e.g. `python3.10 <notebook_name>.py`.
