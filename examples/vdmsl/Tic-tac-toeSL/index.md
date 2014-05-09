---
layout: default
title: Tic-tac-toe
---

~~~
A standard Tic-tac-toe game
#******************************************************
~~~
###XO.vdmsl

{% raw %}
~~~
--
module XO
types
	Pos ::									-- A position for a move
	Game = map Pos to Player;				-- A game (who has moved where)

values
	winningLines = dunion			-- Sets of Pos for winning lines

functions

	whoWon: Game -> Player

	isWon: Game -> bool

	isDraw: Game -> bool

	isUnfinished: Game -> bool

	movesSoFar: Game -> set of Pos

	moveCountSoFar: Game -> nat

	moveCountLeft: Game -> nat

	movesForPlayer: Game * Player -> set of Pos

values
types
	PlayOrder = seq1 of Player				-- The order of play of the players

state Sigma of

operations

	play: PlayOrder * Moves ==> Player | <DRAW> | <UNFINISHED>
		for m in moves do
				if isWon(game) then
		return <UNFINISHED>
end XO
~~~{% endraw %}

###XOTests.vdmsl

{% raw %}
~~~
--
module XOTests
exports all
-- Test data and supporting operations/traces
values
	T1 = [mk_Pos(1,1), mk_Pos(1,2), mk_Pos(2,1), mk_Pos(1,3), mk_Pos(3,1)];
	S = {1, ..., SIZE}
operations
traces
end XOTests
~~~{% endraw %}
