# Hacker-rank-problems(Snake and ladder)
from collections import deque

def quickestWayUp(ladders, snakes):
    board = {}
    for ladder in ladders:
        board[ladder[0]] = ladder[1]

    for snake in snakes:
        board[snake[0]] = snake[1]

    queue = deque()
    queue.append(1)

    visited = [False] * 101
    visited[1] = True

    distance = [0] * 101

    while queue:
        current = queue.popleft()

        for dice in range(1, 7):
            next_cell = current + dice

            if next_cell > 100:
                continue

            if next_cell in board:
                next_cell = board[next_cell]

            if not visited[next_cell]:
                visited[next_cell] = True
                distance[next_cell] = distance[current] + 1

                if next_cell == 100:
                    return distance[next_cell]

                queue.append(next_cell)

    return -1
t = int(input())

for _ in range(t):
    n = int(input())

    ladders = []
    for _ in range(n):
        a, b = map(int, input().split())
        ladders.append([a, b])

    m = int(input())

    snakes = []
    for _ in range(m):
        a, b = map(int, input().split())
        snakes.append([a, b])

    print(quickestWayUp(ladders, snakes))


