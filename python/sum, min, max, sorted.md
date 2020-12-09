# sum, min, max, sorted

```python
lst = [1, 2, 3, 4, -1, 100]

print(sum(lst))  # 109
print(min(lst))  # 01
print(max(lst))  # 100
print(sorted(lst))  # [-1, 1, 2, 3, 4, 100]
print(sorted(lst, reverse=True))  # [100, 4, 3, 2, 1, -1]

lst = (1, 2, 3, 4, -1, 100)

print(sum(lst))  # 109
print(min(lst))  # 01
print(max(lst))  # 100
print(sorted(lst))  # [-1, 1, 2, 3, 4, 100]

lst = "EABCD"
# print(sum(lst))  #TypeError: unsupported operand type(s) for +: 'int' and 'str'
print(min(lst))  # A
print(max(lst))  # E
print(sorted(lst))  # ['A', 'B', 'C', 'D', 'E']
```

