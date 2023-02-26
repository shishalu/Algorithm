# 1244 스위치 켜고 끄기

- IM 대비 문제
- 문제 조건, 입력 부분 뿐만 아니라 출력까지, 모든 부분을 꼼꼼히 살피자.

```py
N = int(input()) # 스위치 개수
switch_temp = list(map(int, input().split()))
students = int(input())

def status_change(switch_temp, idx):
    if switch_temp[idx]:
        switch_temp[idx] = 0
    else:
        switch_temp[idx] = 1

for _ in range(students):
    gender, num = map(int, input().split())

    if gender == 1: # 남학생
        for idx in range(N):
            if not (idx + 1) % num:
                status_change(switch_temp, idx)

    elif gender == 2: # 여학생
        idx = num - 1
        status_change(switch_temp, idx)

        j = 1
        while 0 <= idx - j and idx + j <= N - 1:
            if switch_temp[idx - j] == switch_temp[idx + j]:
                status_change(switch_temp, idx - j)
                status_change(switch_temp, idx + j)
            else:
                break
            j += 1

div = 20
end_pos = N
start_pos = 0
while start_pos < end_pos:
    if start_pos + div > end_pos:
        out = switch_temp[start_pos:end_pos]
    else:
        out = switch_temp[start_pos:start_pos + div]
    start_pos = start_pos + div
    print(*out)
```