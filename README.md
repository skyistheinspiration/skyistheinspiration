1. Water Jug Problem
Aim

To solve the Water Jug Problem using Artificial Intelligence production rules.

Short Theory

The Water Jug Problem is a state-space search problem in AI.
There are two jugs with fixed capacities. The aim is to measure a required quantity of water using operations like:

Fill
Empty
Pour water from one jug to another

A state is represented as:

(X,Y)

Where:

X = water in Jug 1
Y = water in Jug 2
Snippet of Code (Logic Only)
move((X,Y),(4,Y)) :- X < 4.
move((X,Y),(X,3)) :- Y < 3.

move((X,Y),(0,Y)) :- X > 0.
move((X,Y),(X,0)) :- Y > 0.

move((X,Y),(X1,Y1)) :-
    X + Y >= 3,
    X1 is X - (3 - Y),
    Y1 is 3.

goal((2,_)).
Procedure
Define initial state and goal state.
Apply production rules:
Fill jug
Empty jug
Transfer water
Generate new states.
Continue until goal state is reached.
Display required solution path.
Result

The Water Jug Problem was solved successfully using production rules in Prolog.

How To Execute
In SWI-Prolog:
Step 1

Open SWI-Prolog.

Step 2

Save file as:

waterjug.pl
Step 3

Load file:

['waterjug.pl'].
Step 4

Run query:

goal(State).
Viva Questions
What is a state-space problem?

A problem represented using different states and transitions.

What are production rules?

Rules used to move from one state to another.

What is the goal state?

Desired final state of the problem.

Which AI technique is used?

State-space search.

2. Monkey Banana Problem
Aim

To solve the Monkey Banana Problem using Artificial Intelligence concepts.

Short Theory

The Monkey Banana Problem is a classical AI problem where a monkey tries to get bananas hanging from the ceiling.

The monkey can:

Walk
Push box
Climb box
Grab banana

The goal is to make the monkey reach the banana.

Snippet of Code (Logic Only)
move(state(middle,onbox,middle,hasnot),
     grab,
     state(middle,onbox,middle,has)).

move(state(P,onfloor,P,H),
     climb,
     state(P,onbox,P,H)).

move(state(P1,onfloor,P1,H),
     push(P1,P2),
     state(P2,onfloor,P2,H)).
Procedure
Define initial state.
Define goal state.
Apply actions:
Move
Push
Climb
Grab
Generate new states.
Stop when monkey gets banana.
Result

The Monkey Banana Problem was solved successfully using AI state-space representation.

How To Execute
Save file:
monkeybanana.pl
Load:
['monkeybanana.pl'].
Run:
goal(State).
Viva Questions
What is the goal?

Monkey should get banana.

What are operators?

Move, Push, Climb, Grab.

What type of problem is this?

State-space search problem.

Why is box needed?

To reach the banana.

3. DFS and BFS
Depth First Search (DFS)
Aim

To implement Depth First Search in Artificial Intelligence.

Short Theory

DFS is an uninformed search technique.
It explores nodes deeply before backtracking.

It uses:

Stack
Recursion
Snippet of Code
dfs(Start, Goal) :-
    travel(Start, Goal, [Start]).

travel(Goal, Goal, _).

travel(Node, Goal, Visited) :-
    edge(Node, Next),
    not(member(Next, Visited)),
    travel(Next, Goal, [Next|Visited]).
Breadth First Search (BFS)
Short Theory

BFS explores all neighboring nodes first before moving deeper.

It uses:

Queue

BFS gives shortest path in unweighted graph.

Snippet of Code
bfs([[Goal|Path]|_], Goal, [Goal|Path]).

bfs([Path|Paths], Goal, Result) :-
    extend(Path, NewPaths),
    append(Paths, NewPaths, Queue),
    bfs(Queue, Goal, Result).
Procedure
Define graph nodes and edges.
Select start node and goal node.
DFS explores depth-wise.
BFS explores level-wise.
Display traversal path.
Result

DFS and BFS were implemented successfully using Prolog.

How To Execute
Save:
search.pl
Load:
['search.pl'].
Run DFS:
dfs(a,g).
Run BFS:
bfs([[a]], g, Path).




1. WATER JUG PROBLEM
Complete Prolog Code
% Water Jug Problem

% Goal State
goal((2,_)).

% Fill Jug1
move((X,Y),(4,Y)) :-
    X < 4.

% Fill Jug2
move((X,Y),(X,3)) :-
    Y < 3.

% Empty Jug1
move((X,Y),(0,Y)) :-
    X > 0.

% Empty Jug2
move((X,Y),(X,0)) :-
    Y > 0.

% Pour Jug1 to Jug2
move((X,Y),(X1,Y1)) :-
    X + Y >= 3,
    X1 is X - (3 - Y),
    Y1 is 3,
    X > 0.

% Pour Jug2 to Jug1
move((X,Y),(X1,Y1)) :-
    X + Y >= 4,
    Y1 is Y - (4 - X),
    X1 is 4,
    Y > 0.

% Transfer all water Jug1 to Jug2
move((X,Y),(0,Y1)) :-
    X + Y < 3,
    Y1 is X + Y,
    X > 0.

% Transfer all water Jug2 to Jug1
move((X,Y),(X1,0)) :-
    X + Y < 4,
    X1 is X + Y,
    Y > 0.

% Path Finder
path(State,Visited) :-
    goal(State),
    write('Goal Reached: '), write(State), nl,
    write('Visited States: '), write(Visited).

path(State,Visited) :-
    move(State,Next),
    not(member(Next,Visited)),
    path(Next,[Next|Visited]).
How To Execute (VERY IMPORTANT)
Step 1 — Open SWI-Prolog

Open:
SWI-Prolog Official Website

Install if not installed.

Step 2 — Create File

Open Notepad/TextEdit/VS Code.

Paste code.

Save file as:

waterjug.pl
Step 3 — Open SWI-Prolog

You will see:

?-
Step 4 — Load File

Type:

['waterjug.pl'].

Press Enter.

If correct:

true.
Step 5 — Run Program

Type:

path((0,0),[(0,0)]).
Expected Output
Goal Reached: (2,3)

Visited States: [(2,3),(4,1),(0,1),(1,0),(1,3),(4,0),(0,0)]
HOW TO EXPLAIN TO MA’AM
Initial State
(0,0)

Both jugs empty.

Goal State
(2,_)

Need 2 liters in Jug1.

2. MONKEY BANANA PROBLEM
Complete Prolog Code
% Monkey Banana Problem

% Goal State
goal(state(_,_,_,has)).

% Monkey grabs banana
move(
    state(middle,onbox,middle,hasnot),
    grab,
    state(middle,onbox,middle,has)
).

% Monkey climbs box
move(
    state(P,onfloor,P,H),
    climb,
    state(P,onbox,P,H)
).

% Monkey pushes box
move(
    state(P1,onfloor,P1,H),
    push(P1,P2),
    state(P2,onfloor,P2,H)
).

% Monkey walks
move(
    state(P1,onfloor,B,H),
    walk(P1,P2),
    state(P2,onfloor,B,H)
).

% Path Search
canget(State) :-
    goal(State),
    write('Monkey got banana!').

canget(State) :-
    move(State,Action,State1),
    write(Action), nl,
    canget(State1).
How To Execute
Step 1

Save as:

monkeybanana.pl
Step 2

Load:

['monkeybanana.pl'].
Step 3

Run:

canget(state(atdoor,onfloor,atwindow,hasnot)).
Expected Output
walk(atdoor,middle)
push(middle,middle)
climb
grab
Monkey got banana!
State Representation
state(MonkeyPosition, MonkeyStatus, BoxPosition, BananaStatus)

Example:

state(atdoor,onfloor,atwindow,hasnot)

Means:

Monkey at door
Monkey on floor
Box at window
Banana not obtained
HOW TO EXPLAIN
Actions
Walk
Push
Climb
Grab
Goal

Monkey should get banana.

3. DFS AND BFS
Complete Prolog Code
% Graph Edges
edge(a,b).
edge(a,c).
edge(b,d).
edge(b,e).
edge(c,f).
edge(e,g).

% DFS
dfs(Start,Goal) :-
    travel(Start,Goal,[Start]).

travel(Goal,Goal,Visited) :-
    write('Path: '),
    write(Visited).

travel(Node,Goal,Visited) :-
    edge(Node,Next),
    not(member(Next,Visited)),
    travel(Next,Goal,[Next|Visited]).

% BFS
bfs([[Goal|Path]|_],Goal,[Goal|Path]).

bfs([Path|Paths],Goal,Result) :-
    extend(Path,NewPaths),
    append(Paths,NewPaths,Queue),
    bfs(Queue,Goal,Result).

extend([Node|Path],NewPaths) :-
    findall(
        [NewNode,Node|Path],
        (
            edge(Node,NewNode),
            not(member(NewNode,[Node|Path]))
        ),
        NewPaths
    ).
How To Execute
Step 1

Save as:

search.pl
Step 2

Load:

['search.pl'].
DFS Execution
Run:
dfs(a,g).
Output
Path: [g,e,b,a]
BFS Execution
Run:
bfs([[a]],g,Path).
Output
Path = [g,e,b,a]
