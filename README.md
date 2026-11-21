# Build the best Sokoban solver

A push-optimal Sokoban solver: it splits each level into its hallway and rooms, solves every room with A* over pushes, and stitches the room solutions into one move string.

Bounty: https://make.fun/bounty/sokoban-solver-01-run-20261121

![rank](https://make.fun/badge/sokoban-solver-01-run-20261121/RizkyRizk/sokoban-solver-01-run-20261121/rank.svg)
![reward](https://make.fun/badge/sokoban-solver-01-run-20261121/RizkyRizk/sokoban-solver-01-run-20261121/reward.svg)
![make.fun](https://make.fun/badge/sokoban-solver-01-run-20261121.svg)

## How it works

Each level is a hallway with rooms opening off it, and a box that leaves its room can never be pushed back — so rooms are independent and the level optimum is the sum of the room optima. The solver finds the rooms by cutting the hallway row out of the floor graph (each pocket with boxes is a room, its one mouth cell is the door), then solves each room on its own with A* over push states. A state is the sorted box positions plus the player's reachable region, the heuristic is the cheapest matching of boxes to goals, and dead positions are pruned with dead squares, 2x2 blocks and frozen-box detection. Rooms are solved in a fixed order; the player walks between them through the hallway, and the whole answer is replayed on the original level before it is written out. The search budget is a fixed expansion cap, never the clock, so repeated runs produce byte-identical output.
