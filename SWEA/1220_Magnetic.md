```py
for test_case in range(1, 11):
    N = int(input()) # N : 정사각형 테이블의 한 변의 길이

    # 1 : N극
    # 2 : S극
    # 테이블의 윗부분 N극, 테이블의 아래부분 S극

    # 교착 상태의 개수를 출력
    # 2 (아래쪽) 2121 (위쪽) 1
    # 만약에 위에서 2가 나올 경우 그냥 지나가야 한다
    # 하나의 열 탐색이 current = 2로 끝난 경우 마지막 cnt 제외해주어야 한다

    # 일단 array 다 받아보지뭐
    arr = [list(map(int, input().split())) for _ in range(100)]
    cnt = 0
    current = 1
    for i in range(N):
        if current == 2:
            cnt -= 1
            current = 1
        for j in range(N):
            if arr[j][i] == current: # 1을 만났을때부터 반응하자
                current = 2 if current == 1 else 1
                cnt += 1

    print(f'#{test_case}', cnt//2)
    # 얼탱이 없네 이게 왜 정답이 나오지
    # 웃긴다 이게 맞네
```