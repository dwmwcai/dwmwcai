# exp3

```
graph = {
    'A': ['B', 'C', ],
    'B': ['D', 'E'],
    'C': ['F', 'G'],
    'D': [],
    'E': [],
    'F': [],
    'G': []
}

visited = []
queue = []


def bfs(graph, visited, queue, node):
    visited.append(node)
    queue.append(node)

    while len(queue) != 0:
        u = queue.pop(0)
        print(u, end=" ")

        for v in graph[u]:
            if v not in visited:
                visited.append(v)
                queue.append(v)


print("Following is the BFS")
bfs(graph, visited, queue, 'A')
```

# exp4

```
from queue import PriorityQueue
v = 26
graph = [[] for i in range(v)]


def best_first_search(actual_Src, target, n):

    visited = [False] * n
    pq = PriorityQueue()
    pq.put((0, actual_Src))
    visited[actual_Src] = True
    while pq.empty() == False:
        u = pq.get()[1]
        print(chr(u+65), end=" -> ")
        if u == target:
            break
        for v, c in graph[u]:
            if visited[v] == False:
                visited[v] = True
                pq.put((c, v))
    print()


def addedge(x, y, cost):

    graph[x].append((y, cost))
    graph[y].append((x, cost))


addedge(18, 0, 3)
addedge(18, 1, 2)
addedge(0, 2, 4)
addedge(0, 3, 1)
addedge(1, 4, 3)
addedge(1, 5, 1)
addedge(4, 7, 5)
addedge(5, 8, 3)
addedge(5, 6, 2)
source, target = 18, 6
print("The shorest path with less cost form S to G is : ", end="")
best_first_search(source, target, v)
```

# exp5

```

def findLocalMaxima(arr, n):
    mx = []
    if arr[0] > arr[1]:
        mx.append([0, arr[0]])
    for i in range(1, n-1):
        if arr[i-1] < arr[i] > arr[i+1]:
            mx.append([i, arr[i]])
    if arr[-1] > arr[-2]:
        mx.append([n-1, arr[n-1]])
    if len(mx) > 0:
        for i in mx:
            print("Local maxima at position:", i[0], "is", i[1])
    else:
        print("There are no points of local Maxima")


arr = [2, 9, 3, 8, 7, 5, 4, 5, 3]
n = 9
findLocalMaxima(arr, n)

```

# exp6

```
def currentBoard(board):
    print("Current Board:")
    for i in range(9):
        if i > 0 and i % 3 == 0:
            print("")
        if board[i] == 0:
            print("-", end=" ")
        if board[i] == 1:
            print("X", end=" ")
        if board[i] == -1:
            print("O", end=" ")
    print("")


def analyzeBoard(board):
    wb = [[0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6],
          [1, 4, 7], [2, 5, 8], [0, 4, 8], [2, 4, 6]]
    for i in wb:
        if (board[i[0]] != 0 and board[i[0]] == board[i[1]] and board[i[0]] == board[i[2]]):
            return board[i[2]]
    return 0


def user1Turn(board): 
    pos = int(input("X's Turn Enter a Position from 1 to 9  "))
    if board[pos-1] != 0:
        print("Wrong Move!!!")
        exit(0)
    board[pos-1] = 1


def user2Turn(board):
    pos = int(input("O's Turn Enter a Position from 1 to 9  "))
    if board[pos-1] != 0:
        print("Wrong Move!!!")
        exit(0)
    board[pos-1] = -1


print("Game Start:")
board = [0]*9
for i in range(9):
    if (analyzeBoard(board) != 0):
        break
    currentBoard(board)
    if(i % 2 == 0):
        user1Turn(board)
    else:
        user2Turn(board)


x = analyzeBoard(board)

if x == 0:
    currentBoard(board)
    print("Draw!!!")
elif x == 1:
    currentBoard(board)
    print("X Wins!!!")
elif x == -1:
    currentBoard(board)
    print("O Wins!!!")

```

# exp7

```
sudo add-apt-repository ppa: swi-prolog/stable
sudo apt-get update  
sudo apt-get install swi-prolog
swipl
swipl-s filename.pl
%teaches(X, Y): person X teaches in course Y
teaches(sudhir, course001).
teaches(tapas, course002).
teaches(pranab, course003).
teaches(joydeb, course004).

%student(X, Y): student X studies in course Y
studies(suparna, course001).
studies(santanu, course001).
studies(sudip, course002).
studies(sudip, course003).
studies(srobona, course003).
studies(subir, course003).
studies(swarup, course003).

?
teaches(sudhir,X).
teaches(X, Y).
teaches(X, course001).
studies(sudip,X).
studies(X, Y).
studies(X, course001).

%monkey wants to eat banana
on(floor,monkey).
on(floor,box).
in(room,monkey).
in(room,box).
in(room,banana).
at(ceiling,banana).
strong(monkey).
grasp(monkey).
climb(monkey,box).
push(monkey,box):-
    strong(monkey).
under(banana,box):-
    push(monkey,box).
canreach(banana,monkey):-
    at(floor,banana);
    at(ceiling,banana),
    under(banana,box),
    climb(monkey,box).
canget(banana,monkey):-
    canreach(banana,monkey),grasp(monkey).
?
on(floor, box).
in(room, monkey).
trace.
```

# exp8

```
# bayes theorem
def probabilityOfRed(a):

    return a[0]/a[-1]


def probabilityOfBlue(a):

    return a[1]/a[-1]


def numerical(pa, pb, pc, pall, boxinput, colorinput):

    if boxinput == 1 and colorinput == 'red':
        return (pall*probabilityOfRed(pa))/((pall*probabilityOfRed(pa)+(pall*probabilityOfRed(pb))+(pall*probabilityOfRed(pc))))

    if boxinput == 1 and colorinput == 'blue':
        return (pall*probabilityOfBlue(pa))/((pall*probabilityOfBlue(pa))+(pall*probabilityOfBlue(pb))+(pall*probabilityOfBlue(pc)))

    if boxinput == 2 and colorinput == 'red':
        return (pall*probabilityOfRed(pb))/((pall*probabilityOfRed(pa)+(pall*probabilityOfRed(pb))+(pall*probabilityOfRed(pc))))

    if boxinput == 2 and colorinput == 'blue':
        return (pall*probabilityOfBlue(pb))/((pall*probabilityOfBlue(pa))+(pall*probabilityOfBlue(pb))+(pall*probabilityOfBlue(pc)))

    if boxinput == 3 and colorinput == 'red':
        return (pall*probabilityOfRed(pc))/((pall*probabilityOfRed(pa)+(pall*probabilityOfRed(pb))+(pall*probabilityOfRed(pc))))

    if boxinput == 3 and colorinput == 'blue':
        return (pall*probabilityOfBlue(pc))/((pall*probabilityOfBlue(pa))+(pall*probabilityOfBlue(pb))+(pall*probabilityOfBlue(pc)))


box1 = [3, 2, 5]
box2 = [4, 5, 9]
box3 = [2, 4, 6]
pofall = 1/3
colorinput = input("Enter the color of the ball: ")
boxinput = int(input("Enter a box number: "))
print("The Probabilty will be: ")
print(numerical(box1, box2, box3, pofall, boxinput, colorinput))

```

# exp9

```
# p(3/A)=a, p(M/A)=b, p(A/-8,-E)=c, p(-8)=d, p(-E)=e
# p(J/A)*p(A)=f, p(3/-A)=g, p(J/-A) *p(-A)=h

p_JA = 0.9
p_MA = 0.7
p_ABE = 0.001
p_B = 0.999
p_E = 0.998
p_JAA = 0.00252
p_JA1 = 0.05
p_JAA1 = 0.9974
probability = p_JA * p_MA * p_ABE * p_B * p_E
probability2 = p_JA * p_JAA + p_JA1 * p_JAA1
print("probability of john and merry both call ", probability)
print("The probability distribution where all the events are given is less than 0.05")
print("probability of call is ", probability2)
print("The probability distribution where all the events are given is less than 0.05")
```
