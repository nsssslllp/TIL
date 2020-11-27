# 구현
대표문제1) 상하좌우   
시뮬레이션 유형 (일련의 명령 따라 개체를 차례대로 이동)
```python
n=int(input())
go=input().split()
#map object is not subscriptable
#go=list(map(str,input().split()))
i=1
j=1
for g in go:
    if g=='L' and i>1:
        j-=1
    if g=='R' and i<n:
        j+=1
    if g=='U' and i>1:
        i-=1
    if g=='D' and i<n:
        i+=1
    
print(str(i)+' '+str(j))


#파이썬에서 문자열 자료형은 str
'''문자열 입력받고 문자 리스트로 저장:
    go=input().split()
( 굳이 go=list(map(str,input().split()))처럼
  str로 안바꿔도 원래 str임)
'''
#그냥 map으로 묶으면 인덱스로 접근 불가능 
#문자 쓸 때 ''나 "" 꼭 

SOL)
이게 문제의 의미를 더 잘 살림
dx=[0,0,-1,1]
dy=[-1,1,0,0]
move_types=['L','R','U','D']

for p in go:
    for i in range(len(move_types)):
        if plan==move_types[i]: #이동 후 좌표 구하기
            nx=x+dx[i]
            ny=y+dy[i]
    #공간 벗어날 때 무시
    if nx<1 or ny<1 or nx>n or ny>n:
        continue
    x,y=nx,ny #이동 수행
print(x,y)
```

예제2) 시각
정수N이 입력되면 00시00분00초부터 N시59분59초까지-3포함 시각 출력
