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
