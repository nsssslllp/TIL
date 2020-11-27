# Greedy Algorithm
-지금 당장 좋은 것만 선택(나중 영향x)  
-종류)다익스트라 알고리즘..  
-키워드) 가장 큰/작은 순서대로 (정렬)

대표 문제) 거스름돈
```python
# 최소 코인 개수로 n원 만들기
n=1260
count=0

#큰 단위 화폐부터 차례대로 확인
for coin in list:
    count+=n//coin #해당 화폐로 거슬러 줄 수 있는 동전 개수 세기
    n %= coin

print(count)
##시간복잡도: O(동전종류 수)
'''그리디 알고리즘 쓴 이유
 1) 가장 큰 화폐부터
 2) 큰 단위가 작은 단위의 배수 (무작위->다이나믹 프로그래밍.)
'''
```

실전문제2)큰 수의 법칙
```python
# k번 연속 더하기 가능-> m번 연산으로 최대값 만들기
n,m,k=map(int,input().split())
input_data=list(map(int,input().split()))

input_data.sort()
sum=0
count=0

n,m,k=map(int,input().split())
input_data=list(map(int,input().split()))

input_data.sort()
sum=0
count=0

while count<m:    
    for i in range(k):    
        if count<m:
            sum+=input_data[n-1]
            count+=1
        else:
            break
    
    if count<m:
        sum+=input_data[n-2]
        count+=1

    
print(sum)


''' 처음
while count<=m:
    sum+=input_data[n-1]*k
    count+=k
    sum+=input_data[n-2]
    count+=1
print(count)

>>반복문 도중에 count==m이 되어도 멈추지 않음
'''
'''
else: break 말고 break을 넣었더니 count<m인 경우에도 if문 지난다음 break해버림
else: break을 안쓰면 count<m인지 k번을 다 확인함
'''

#SOL1)
fist=input_data[n-1]
second=input_data[n-2]
while True:
    for i in range(k): #가장 큰 수 k번 더하기
        if m==0: #m이 0이면 반복문 탈출
            break
        result+=first
        m-=1
    if m==0:
        break
    result+=second
    m-=1

#SOL2) 가장 큰 값이 더해지는 횟수 구하기
count=int(m/(k+1))*k #first k개와 second 1개가 한 쌍
count+=m%(k+1)

result=0
result+=(count)*first
result+=(m-count)*second
```

실전문제3) 숫자 카드 게임
```python
#각 행에서 min값 뽑아 그 중 최대값 출력
n,m=map(int,input().split())
n_data=[]
m_data=[]
#2차원 리스트 만들기    
for i in range(n):
  m_data=list(map(int,input().split())) #행 리스트(1xm) 입력
  n_data.append(m_data) #각 행에 행 리스트 추가

min_num=[0]*n
for i in range(n):
    min_num[i]=min(n_data[i])

print(max(min_num))
'''
2차원리스트 만드는 문법 헷갈림 -> 부록 보기
문법 오류 나면 그 앞줄도 보기
'''
# SOL1) result=0?
# SOL2) a?
## SOL1, SOL2 질문하기 
```

실전문제4) 1이 될 때까지
```python
# n을 k로 나누거나 1을 빼서 1만드는 최소 연산 수
n,k=map(int,input().split())
count=0

while n!=1:
    if n%k==0:
        n/=k
        count+=1
    else:
        n-=1
        count+=1
print(count)
'''
SOL1)
SOL2)
다시보기 
'''
```