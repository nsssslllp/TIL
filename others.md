# 기타 알고리즘

## 1. 소수판별

```python
# Sol1) 약수(절반만->제곱근까지)로 나누어지지 않으면 소수
def is_prime_number(x):
    #2부터 x의 제곱근까지의 모든 수를 확인하며
    for i in range(2,int(math.sqrt(x))+1):
        #x가 해당 수로 나누어떨어진다면
        if x%i == 0:
            return False #소수 아님
    return True #소수

print(is_prime_number(4))
```

## 2: n까지의 수 중 소수인 것 출력
```python
# 나)
n=int(input())
d=[2]*1

for i in range(3,n+1): #소수 리스트 채우기
    count=0
    for j in range(len(d)): #이미 소수로 판별된 수로 나누기
        if i%d[j]==0:
            count+=1
    if count==0: #한번도 나누어지지 않으면 소수리스트에 추가
        d.append(i)

# 소수판별     
if n in d:
    print("소수입니다")
else:
    print("소수가 아닙니다")

# n까지 수 중 소수 출력
print(d)
```

```python
# 에라토스테네스의 체 : 처리하지 않은 가장 작은 수 i의 배수를 제거
#                      (i는 n의 제곱근까지)
import math

n=1000
array=[True for i in range(n+1)]

for i in range(2,int(math.sqrt(n)+1)): #2부터 n의 제곱근까지의 모든 수 확인하며
    if array[i]==True: #i가 소수인 경우(남은경우)
        #i를 제외한 i의 모든 배수 지우기
        j=2
        while i*j<=n:
            array[i*j]=False
            j+=1
#모든 소수 출력
for i in range(2,n+1):
    if array[i]:
        print(i,end=' ')
```
## 3. 투 포인터 : start, end 이용
### <1. 합이 n인 구간의 개수 찾기>
1) start=end=0  
2) if 현재합=M  -> count+=1
3) if 현재합<M  -> end+=1
4) if 현재합>=M -> start+=1 
5) 모든 경우 확인할 때까지 2~4 반복  
(시작점을 오른쪽으로 이동시키면 항상 합이 감소,   
 끝점을 오른쪽으로 이동시키면 항상 합이 증가함을 이용)

```python
n=5 #데이터의 개수N
m=5 #찾고자 하는 부분합M
data=[1,2,3,2,5] #전체 수열

count=0
interval_sum=0
end=0

#start를 차례대로 증가시키며 반복
for start in range(n):
    #end를 가능한 만큼 이동
    while interval_sum<m and end<n:
        interval_sum+=data[end]
        end+=1
    #부분합이 m일 때 카운트 증가
    if interval_sum==m:
        count+=1
    interval_sum-=data[start]
print(count)
```

### <2. 정렬되어 있는 두 리스트의 합집합 구하기>
ㄴ병합정렬 같은 일부 알고리즘에 사용
 1) 리스트 A에서 처리되지 않은 가장 작은 원소 : A[i]
 2) 리스트 B에서 처리되지 않은 가장 작은 원소 : B[j]
 3) min(A[i],B[j])를 결과 리스트에 추가
 4) 리스트 A,B에 처리할 원소 없을 때까지 2~4 반복
```PYTHON
#시간복잡도 O(N+M)
n,m=3,4
a=[1,3,5]
b=[2,4,6,8]
#리스트 A와 B의 모든 원소를 담을 수 있는 크기의 결과 리스트 초기화
result=[0]*(n+m)
i,j,k=0

#모든 원소가 결과 리스트에 담길 때까지 반복
while i<n or j<m:
    #리스트 B의 모든 원소가 처리되었거나, 리스트A의 원소가 더 작을 때
    if j>=m or (i<n and a[i]<=b[j]):
        #리스트A의 원소를 결과 리스트로 옮기기
        result[k]=a[i]
        i+=1
    #리스트A의 모든 원소가 처리되었거나, 리스트B의 원소가 더 작을 때
    else:
        #리스트B의 원소를 결과 리스트로 옮기기
        result[k]=b[j]
        j+=1
    k+=1

for i in result:
    print(i,end=' ')
```

## 4. 구간 합 계산 <-접두사 합
1) n개의 수에 대해 접두사 합을 계산해 배열P에 저장
2) 매 M개의 쿼리 정보 [L,R]을 확인할 때, 구간 합은 P[R]-P[L-1]
   
```PYTHON
n=5
data=[10,20,30,40,50]

#접두사 합 배열 계산
sum_value=0
prefix_sum=[0]
for i in data:
    sum_value+=i
    prefix_sum.append(sum_value)

#구간 합 계산 (세번째수부터 네번째 수까지)
lef=3
right=4
print(prefix_sum(right)-prefix_sum[left-1])
```

## 5. 순열과 조합 <-itertools 라이브러리 
 1) 순열 nPr : permutations() 함수
 2) 조합 nCr : combinations() 함수
```python
import itertools
data=[1,2,3]

for x in itertools.combinations(data,2):
    print(list(x),end=' ')
```

## 예제
1. M이상 N이하 소수 모두 출력
```python
import math

m,n=map(int,input().split())
array=[True for i in range(n+1)]
array[1]=False

for i in range(2,int(math.sqrt(n)+1)): #2부터 n의 제곱근까지의 모든 수 확인하며
    if array[i]==True: #i가 소수인 경우(남은경우)
        #i를 제외한 i의 모든 배수 지우기
        j=2
        while i*j<=n:
            array[i*j]=False
            j+=1
#모든 소수 출력
for i in range(m,n+1):
    if array[i]:
        print(i)
```

2. C종류 소문자로 L길이 암호 만들 수 있는 모든 경우의 수 (오름차순)
  ```python
  #나)
import itertools

l,c=map(int,input().split())
c_list=list(map(str,input().split()))
m=['a','e','i','o','u']

c_list.sort()
for i in itertools.combinations(c_list,4):
    count=0
    for j in m:
        if j not in i:
            count+=1 #모음개수=count
    if count!=0: #모음개수0개 아니면 출력
        print(''.join(i))
```

```python
# sol)
from itertools import combinations
vowels=['a','e','i','o','u']
l,c=map(int,input().split())

array=input().split(' ')
array.sort()

#길이가 1인 모든 암호 조합 확인
for password in combinations(array,1):
    #패스워드에 포함된 각 문자를 확인하며 모음 개수 세기
    count=0
    for i in password:
        if i in vowels:
            count+=1
    #최소 1개의 모음과 2개의 자음이 있는 경우 출력:
    if count>=1 and count<=1 -2 :
        print(''.join(password))
```
