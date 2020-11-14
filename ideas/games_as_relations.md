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

For simplicity sake, we will say that there is no ties.
A player loses a game, when it reaches a state that is not 
a __ContinueState__. Let's call it __EndState__.

If you give a jumbled chess board to two player and say, 
play chess with the normal rules. They will play it 
(after they decide which one is who). 
But if we want a relation between 2 __Strategy__, saying 
who is better, we need a __GameInit__ to figure that out,
if not, then a __Strategy__ could win and lose to other 
__Strategy__.

    S, T ∈ Strategy
    S ≥ T <=> S beats T (...)

If we imagine the relation ≥ as a directed graph where the
nodes are Strategies, in this graph can exist cycles, so
if we see the SCC's of that graph as a nodes we can see 
which group wins to which group, Because we have a DAG.

If it exists only winners and losers in the game, then 
that graph is going to be a serial relation.

Example:
(To be written)
