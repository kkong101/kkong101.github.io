---
layout: post
title:  "테스트 업로드"
categories: JavaScript
tags: JavaScript
author: KKong
---

* content
{:toc}

테스트를 해보겠습니다.













{% raw %}
## 본격 설명 시작 

[**문제 링크**](https://www.acmicpc.net/problem/1012)



2차원 배열에 input으로 1를 입력받고,  상하좌우 기준으로 1이 인접되어있는 cluster의 갯수를 찾는게 문제이다.

이 문제를 효율적으로 해결하기 위해 깊이 우선 탐색(DFS) 알고리즘을 이용하여 문제를 해결했다. 



> **문제 해결 Process**
>
> 1.  테스트 케이스 T,  가로 M, 세로 N, 배추 갯수 K 입력 받기
> 2.  M * N 크기의 0으로 이루어진 2차원 배열 생성(field)
> 3.  2차원 리스트(field)에  K개의 배추의 위치를 1값으로 입력 
> 4. field[0,0] 부터 차례대로 for문을 돌아서 1이면 현재 좌표의 파라미터를 넣어준 dfs 함수 호출, cnt 1증가
> 5. 호출되면 일단 1이였던 값을 2로 변경(방문했다는 표시)
> 6. 상하좌우의 위치를 넣어준 dx,dy 리스트를 돌면서 인접된 곳에 1이 있는지 확인
> 7. 인접된곳에 1이 발견이 되었다면 자기 자신(dfs 함수)을 다시 호출 
> 8. 인접된 곳이 모두 2로 바뀌며 하나의 cluster 찾기를 완료함 (한개의 덩어리 => cnt : 1)
> 9. 다른 cluster을 찾아 위와 같이 동일하게 반복 (cnt += 1로 갯수 counting)



```python
import sys
sys.setrecursionlimit(10**6)

test_case = int(input())
dx = [-1,0,1,0]
dy = [0,1,0,-1]

def dfs(i,j):
    field[i][j] = 2
    for ii in range(4):
        rx, ry = i + dx[ii] , j + dy[ii]
        if rx < 0 or rx >= M or ry < 0 or ry >= N:
            continue
        elif field[rx][ry] == 1:
            dfs(rx,ry)
result_list = []

for _ in range(test_case):
    N, M, K = map(int, input().split())
    cnt = 0
    field = [[0 for _ in range(N)] for _ in range(M)]
    for _ in range(K):
        x,y = map(int,input().split())
        field[y][x] = 1
    for i in range(M):
        for j in range(N):
            if field[i][j] == 1:
                dfs(i,j)
                cnt += 1
    result_list.append(cnt)

for e in result_list:
    print(e)


```



각각의 Process를 머릿속에 생각하시면서 위의 코드를 보시면 이해에 도움이 되실겁니다. 


{% endraw %}
