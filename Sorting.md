# 정렬
-이진 탐색의 전처리 과정  
-reverse메서드(오름<->내림):O(N)

<br/>  
(오름차순, 데이터개수:N)  

## 1 선택 정렬 : '가장 작은 것을 앞으로' * (N-1)
- 가장 작은 것을 맨앞으로, 남은 n-1개 중 가장 작은 것을 두번째로...  
- 마지막 데이터는 이미 정렬됨 -> n-1번 연산   
- 현재 데이터 상태 관계없이 무조건 모든 원소 비교하고 스왚->비효율적
- 소스코드)  
```PYTHON
array=[7,5,9,0,3,1,6,2,4,8]
for i in range(len(array)): #N-1번 반복
    min_index=i #가장 작은 원소의 인덱스 (최솟값 넣을 곳)
    for j in range(i+1,len(array)): #정렬되지 않은 것들과
        if array[min_index] > array[j]: #min_index 원래 원소와 비교
            min_index=j                   #더 작은 걸 min_index에 
    array[i],array[min_index]=array[min_index],array[i] #스와프
print(array)
```
*시간복잡도는 반복의 중첩을 기준으로
- 시간 복잡도 : O(N^2)  
  (2중반복문)   
  >{n+(n-1)+(n-2)+...+2} = (n+2)(n-1)/2   
  (min: 연산 n번->n-1번->...->2번) (min구하는 걸 n-1번)  
 

<BR/>
<BR/>

## 2 삽입 정렬 : '작은 수 옆으로 이동' * (N-1)
- 앞서 정렬된 데이터들(오름차순) 중 자기 자리 찾기  
   = 자기보다 작은거 만날 때까지 이동
- 첫 원소는 정렬 가정 -> N-1번 연산
- 필요할 때만 위치 바꿈 -> **데이터 거의 정렬돼 있을 때** 효율적
- 속도 : 나머지>>삽입정렬>>>>선택정렬  
- 소스코드)
```PYTHON
  array=[7,5,9,0,3,1,6,2,4,8]
  for i in range(1,len(array)): #N-1번 반복
    for j in range(i,0,-1): #인덱스 i부터 1까지 1씩 감소하며 반복
        if array[j]<array[j-1] #큰놈만나면 
            array[j],array[j-1]=array[j-1],array[j] #이동
        else: #작은놈만나면
            break #거기가 자기 자리
  print(array)

  #range(start,end,step) :step=-1이면 start부터 "end+1"까지 감소
```

- 시간복잡도: O(N^2), 최선 O(N)  
(2중반복문)  
  최악의 경우(내림차순-늘 가장 우측값이 최소): 이동 N-1번-> N-2번->...->2번  
  >(N-1)+(N-2)+...+2=(N+2)(N-1)/2  
 최선의 경우(오름차순-이동안함): for j 반복문 노쓸모  
 
  **거의 정렬돼 있을 때 쓰자**
<br/>
<br/>


## 3 퀵 정렬 : 피벗보다 큰 수와 작은 수 교환  
  ### 中 호어 분할 방식: 첫 원소가 피벗  
         1) 왼쪽부터 피벗보다 큰수, 오른쪽부터 피벗보다 작은수 찾아 교환
         2) 둘이 위치 엇갈리면, 작은수와 피벗 교환  
           -> 피벗 좌측: 피벗보다 작은 수들. 우측: 큰 수들
         3) 피벗 좌,우측도 1)2) 반복해 정렬
         4) 현재 리스트 개수가 1될 때까지 3)반복 
- 소스코드)
```python
array=[5,7,9,0,3,1,6,2,4,8]

def quick_sort(array,start,end):
    if start>=end: #원소 1개인 경우 종료
        return
    pivot=start #피벗은 첫번째 원소
    left=start+1
    right=end
    while left<=right:
        #피벗보다 큰 데이터를 찾을 때까지 반복
        while left<=end and array[left]<=array[pivot]: #left랑 피벗 같아도 됨
            left+=1
        #피벗보다 작은 데이터를 찾을 때까지 반복
        while right>start and array[right]>=array[pivot]: #등호 왜?
            right-=1
        if left>right: #엇갈렸다면 작은 데이터와 피벗 교체
            array[right],array[pivot]=array[pivot],array[right]
        else: #엇갈리지 않았다면 작은 데이터와 큰 데이터 교체
            array[left],array[right]=array[right],array[left]
     #분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
     quick_sort(array,start,right-1)
     quick_sort(array,right+1,end)

     quick_sort(array,0,len(array)-1)
     print(array)   
```
```python
#파이썬 장점 살린 좀 더 느린 퀵 정렬 소스코드
def quick_sort(array):
    #리스트가 하나 이하의 원소만을 담고 있다면 종료
    if len(array)<=1:
        return array
    
    pivot=array[0] #피벗은 첫번째 원소
    tail=array[1:]

    left_side=[x for x in tail if x<=pivot] #분할된 왼쪽 부분
    right_side=[x for x in tail if x>pivot] #분할된 오른쪽 부분

    #분할 이후 왼쪽과 오른쪽 각각 정렬수행,, 전체 리스트 반환
    return quick_sort(left_side)+[pivot]+quick_sort(right_side)

print(quick_sort(array))
```
- 시간복잡도: 평균 O(NlogN)


## 4 계수 정렬
## 5 파이썬의 정렬 라이브러리


실전문제2) 위에서 아래로
```python
n=int(input())
input_data=[]
for i in range(n):
    input_data.append(int(input()))
input_data.sort()
for i in range(n):
    print(input_data[i],end=' ')    

#SOL) 내림차순이니까 reverse
#출력할 때 리스트 값 직접 가져오는게 쉬움
array=sorted(array,reverse=True)
for i in input_data:
    print(i, end=' ')    
```
