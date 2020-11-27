1)금광
```python
n,m=map(int,input().split())
#t=int(input())
store=[[0]*m for _ in range(n)]
#for i in range(t):

gold=list(map(int,input().split()))
for i in range(0,n):
    for j in range(0,m):
        for k in range(0,n*m):
            store[n][m]=gold[k]
print(store)
```        
