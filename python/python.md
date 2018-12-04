# Python

## Dictionary

逐个添加元素到不存在的字典中可以使用`try...except...`

```python
dict = {}
try:
    dict[key].append(value)
except:
    dict[key] = [value]
```
---

## 全局变量和局部变量

1. 函数内不需要声明就可以直接使用外部的全局变量。
2. 如果在函数内声明与全局变量同名的内部变量，则新的内部变量与全局变量无关。
3. 如果想在函数内修改全局变量，修改前使用`global 全局变量名` 即可修改全局变量。