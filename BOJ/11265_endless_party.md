# 11265 끝나지 않는 파티

## 첫번째 시도

- BFS를 이용해 접근해보고자 하였다
- 문제에서 제시된 테스트 케이스는 통과하지만, 채점에서는 시간초과 발생
- 나중에 다시 도전하기로 하였다.. (23.02.26.Sun)

```py
N, M = map(int, input().split())  # N : 파티장의 크기, M : 요청한 손님의 수

party_road = [[0] * (N + 1)] + [[0] + list(map(int, input().split())) for _ in range(N)]
for _ in range(M):
    start, end, total_time = map(int, input().split())
    res = ''
    visited = [[0 for _ in range(N + 1)] for _ in range(N + 1)]
    q = [(start, total_time)]
    while q:
        current, time = q.pop(0)

        if party_road[current][end] <= time:  # 일방통행 도로로 바로 도착할 수 있는 경우
            res = 'Enjoy other party'
            break

        visited[current][end] = 1
        visited[end][current] = 1

        for i in range(1, N):
            if i == end or visited[current][i] == 1:
                continue
            if party_road[current][i] < time:
                visited[current][i] = 1
                visited[i][current] = 1
                q.append((i, time - party_road[current][i]))

    if res == '':
        res = 'Stay here'

    print(res)
```