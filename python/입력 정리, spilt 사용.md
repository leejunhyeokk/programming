# python - 입력 정리, EOF 까지 | 한줄 그냥 | spilt 이용해서

```python

# 문자열 한줄을 그냥 받기
a = input()
print(a)

# 공백을 제외한 알맹쓰만 받기 -> 리스트로 반환됨
a = input().split()
print(a)

# EOF(ctrl+Z) 까지 한줄 한줄 입력받기 (공백 포함 싹다 포함)

# https://www.acmicpc.net/problem/11718
import sys

for line in sys.stdin:
    a = line
    print(a, end='')  # line자체가 enter를 포함학 있다.

# EOF(ctrl+Z) 한번에 입력받기 (공백 포함 싹다 포함)

# https://www.acmicpc.net/problem/11718
import sys
v = sys.stdin.read()
print(v, end='')

# EOF(ctrl+Z) 까지 한줄 한줄 입력받기 (공백 없이 알맹이 문자열만)

import sys

for line in sys.stdin:
    a = line.split()
    print(a)

# EOF(ctrl+Z) 까지 정수 a,b  입력받기

import sys

for line in sys.stdin:
    a, b = map(int, line.split())
    print(a + b)

#  공백 포함 문자열 하나하나 분리하기

a = input()
print(list(a))

#  공백 제거 후 문자열 하나하나 분리하기

a = input().split()
for e in a:
    print(list(e))

#  1234 숫자 입력시 , 1,2,3,4 로 하나씩 끊어 받기 ( 공백 처리 불가능  )

a = list(input())
res = list(map(int, a))

print(res)

#  1234 숫자 입력시 , 1,2,3,4 로 하나씩 끊어 받기 ( 공백 처리 가능 )
ans = []
a = input().split()
for e in a:
    res = list(map(int, e))
    ans.extend(res)

print(ans)

# 뛰어쓰기 처리하기 -> replace('\n','')

import sys

var = sys.stdin.read()
var = (var.replace('\n', '').split(','))
print(sum(list(map(int, var))))

# EOF 까지 한번에 읽어서, 뛰어쓰기는 제거하고 ,로 나눠서 리스트를 반환후 더한값을 출력하기
# https://www.acmicpc.net/problem/10823
import sys

nlist = [int(x) for x in sys.stdin.read().replace('\n', '').split(',')]
print(sum(nlist))
```