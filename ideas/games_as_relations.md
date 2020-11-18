% Games as Relations

We can see a __Game__ as a pair, of a __GameStrategy__ and a __GameInit__.

A __GameStrategy__ is a relation with type 
    GameState -> GameState
.

    type GameStrategy = Rel GameState GameState

A __GameInit__ is a __GameState__.

It can be seen as a graph between states of the game, 
for example in the game of chess, the game state would 
be the board and its pieces, in a given moment (With 
castle and repetition of states, is a bit more, but to
simplify, lets not have that).

Let's say that a player before a game is programmed to 
play in a specific way, which means, that for a specific 
__GameState__ the player will play a specific valid move. 
That player would be undistinguichable from a normal player, 
without taking into account the pressure of the moment.
This "programable player" can be modeled pretty nicelly. 
with only a function between game states, we can also call 
it a __Strategy__, because all that player does is execute 
a strategy.

Lets call __ContinueState__ to the game states which have at 
least one move to another state in the game.

    type Strategy = ContinueState -> GameState

A player wins the game, when it reaches a state that is not 
a __ContinueState__. Let's call it __WinState__.

If you give a jumbled chess board to two player and say, 
play chess with the normal rules. They will play it 
(after they decide which one is who). 
But if we want a relation between 2 __Strategy__, saying 
who is better, we need a __GameInit__ to figure that out,
if not, then a __Strategy__ could win and lose to other 
__Strategy__.

    S, T ∈ Strategy

    S ≥1 T <=> <∃n:: _WinStateº . (S . T)^n . S . _GameInitial ≠ ∅ >
    (S ≥1 T <=> S beats T, when S plays first)

    S ≥2 T <=> <∃n:: _WinStateº . (T . S)^n . T . _GameInitial ≠ ∅ >
    (S ≥2 T <=> S beats T, when S plays second)

The relation ≥1 or ≥2 only exists if there is 2 players.

If we imagine the relation ≥1 or ≥2 as a directed graph where the
nodes are Strategies, in this graph can exist cycles, so
if we see the SCC's of that graph as a nodes we can see 
which group wins to which group, Because we have a DAG.

If it exists only winners and losers in the game, then 
that graph is going to be a serial relation, which means
there exists a group of Strategies that are the best ones.

One important question now is, what is the structure of S 
and T, such that the __S.T__ and __S^n__ is easy to calculate.

Matrices have that property, but then it has to have all of
the __GameStates__ in the row and collumn.

# Example

## Description 

A simple example can be a made up game, that is described 
like the following:

The State of the game is only a number in modulo 5.

    GameState = {0,1,2,3,4}

The initial state is 0.

    GameInitial = 0

The players can sum 1 or 2 to the state.

    GameStrategy = { (a, b) | (b = a+1 ∨ b = a+2) ∧ a≠4 }

The player who reaches 4, wins.

    WinState = { 4 }

The __GameStrategy__ as a matrix:

    |0 0 0 1 0|
    |1 0 0 0 0|
    |1 1 0 0 0|
    |0 1 1 0 0|
    |0 0 1 1 0|

The number of __Strategies__ in this __GameStrategy__
is 2⁴ = 16



## ≥1 and ≥2

    S ≥1 T <=> <∃n:: 4 = ((S . T)^n . S) 0 >
    S ≥2 T <=> <∃n:: 4 = ((T . S)^n . T) 0 >

if we see an S and a T as a binary matrices 5 by 5,
then S and T can be seen as 

    ST = ST1 . DST . ST2, ST2 = ST1⁻¹
    TS = TS1 . DTS . TS2, TS2 = TS1⁻¹

    S ≥1 T <=> <∃n:: 4 = (ST1 . DST^n . ST2 . S) 0 >
    S ≥2 T <=> <∃n:: 4 = (TS1 . DTS^n . TS2 . T) 0 >
    
