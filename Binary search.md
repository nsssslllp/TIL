## 순차 탐색
: 앞에서부터 원소 하나씩 체크  
-  ex) 특정 원소 유무 확인, 원소 개수 세는 count() 메서드 내부  
- 시간복잡도: 최악의 경우 O(N)  
-  특정 원소 인덱스 출력)
 ```python
 def sequential_search(n,target,array):
    #각 원소 하나씩 확인
    for i in range(n):
        #현재원소가 찾고자 하는 원소와 동일할 경우
        if array[i]==target:
            return i+1 #현재위치반환(인덱스는 0부터 시작하므로 1더하기)
```


 # 이진 탐색 : 중간점 데이터와 타겟 데이터 비교 반복
- 선형 재건: 정렬
- 중간점이 실수이면 소수점이하 버림 (//연산자 or int())
- 1) 중간점 데이터와 타겟 데이터 비교  
     if 중간점 데이터 > 타겟 데이터 : 중간점 이후 값 버림  
     if 중간점 데이터 < 타겟 데이터 : 중간점 이전 값 버림  
     if 중간점 데이터 = 타겟 데이터 : 탐색 종료
  2) 타겟 데이터 이동
  3) 시작점,중간점,끝점 갱신
  4) 1,2,3 반복
- 소스코드
```PYTHON
  #1. 재귀함수
  def binary_search(array,target,start,end):
    if start>end: #??
        return None
    mid=(start+end)//2
    #찾은 경우 중간점 인덱스 반환
    if array[mid]==target:
        return mid
    #중간점의 값보다 찾고자 하는 값이 작은 경우 중간점의 왼쪽 확인
    elif array[mid]>target:
        return binary_search(array,target,start,mid-1)
    #중간점의 값보다 찾고자 하는 값이 작은 경우 중간점의 오른쪽 확인
    else:
        return binary_search(array,target,mid+1,end)
  n,target=list(map(int,input().split()))
  array=list(map(int,input().split()))
 
  result=binary_search(array,target,0,n-1) #end=n-1
  if result==None:
    print("원소가 존재하지 않습니다")
  else:
    print(result+1) #인덱스는 0부터시작해서 +1해줘야
 ```

 ```python
 #2. 반복문
  def binary_search(array,target,start,end):
    while start<=end:
        mid=(start+end)//2
        #찾은 경우 중간점 인덱스 반환
        if array[mid]==target:
            return mid
        #중간점의 값보다 찾고자 하는 값이 작은 경우 중간점의 왼쪽 확인
        elif array[mid]>target:
            end=mid-1
        else:
            start=mid+1
    return None #start>end 일때
 
  n,target=list(map(int,input().split()))
  array=list(map(int,input().split()))

  result=binary_search(array,target,0,n-1)
  if result==None:
    print("원소가 존재하지 않습니다.")
  else:
    print(result+1)
 ```

-  시간복잡도: O(logN)  
   한 번 확인할 때마다 확인하는 원소의 개수가 절반씩 줄어듦
<br/>  
  **탐색범위가 2000만 넘어가면** 이진탐색으로 접근해보자   
  이진 탐색 코드는 외워두자

## 트리 자료구조 : 부모노드-자식노드 관계
- 트리의 최상단 노드: 루트 노드
- 트리의 최하단 노드: 단말 노드
- 파일 시스템과 같이 **계층적이고 정렬된 데이터**다루기에 적합
<br/>

## 이진 탐색 트리
- 크기: 왼쪽 자식 노드 < 부모 노드 < 오른쪽 자식 노드
- 이진 탐색 트리가 미리 구현되어 있을 때 조회하는 방법:  
    1) 루트노드 방문->   
      타겟보다 크면: 왼쪽 자식 노드로   
      타겟보다 작으면: 오른쪽 자식 노드로
    2) 타겟값 있는 노드 찾거나, 자식 노드 없을 때까지 반복
   <br/>
   ### *빠르게 입력받기 
   -이진탐색 문제: 입력데이터 많거나(1000만 이상),
                  탐색 범위 매우 넓음(1000억 이상)  
   *sys 라이브러리
    ```python
    import sys
    #하나의 문자열 데이터 입력받기
    #rstrip()함수가 엔터(줄 바꿈) 제거
    input_data=sys.stdin.readline().rstrip()
    print(input_data)
    ```

    실전문제2) 부품 찾기