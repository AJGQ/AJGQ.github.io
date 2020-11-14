% Games as Relations

We can see a game as a relation with type 
    GameState -> GameState
.

    type Game = Rel GameState GameState

It can be seen as a graph between states of the game, 
for example in the game of chess, the game state would 
be the board and its pieces, in a given moment.

Let's say that a player before a game is programmed to 
play in a specific way, wich means, that for a specific 
__GameState__ the player will play a specific valid move. 
That player would be undistinguichable from a normal player, 
without taking into account the pressure of the moment.
This "programable player" can be modeled pretty nicelly. 
with only a function between game states, we can also call 
it a __Strategy__, because all that player does is execute 
a strategy.

Lets call __ContinueState__ to the game states wich have at 
least one move to another state in the game.

    type Strategy = ContinueState -> GameState

For simplicity sake, we will say that there is no ties.
A player loses a game, when it reaches a state that is not 
a ContinueState. Let's call it __EndState__.

Be aware that a game to exist, only needs its rules, without 
the initial state. for example if you give a jumbled chess 
board to two player and say, play chess with the normal rules.
They will play it (after they decide wich one is who).

With this, it can be proven that a strategy can win and lose 
to other strategies. And, in some cases, can be constructed 
a relation between strategies, to say what strategy is the best,

Example:
(To be written)
