---
id: p4cw3v33dale2yxdsnbc1w7
title: List_comprehension
desc: ''
updated: 1753258433890
created: 1753257384238
---


```bash
range(0,10)
list(range(0,10))
new_list.append()

## list comprehension
lst = [2,3,4,5]
[expression for member in iterable]
new_lst = [num*2 for num in lst]
print(new_list)

even_list=[]
for i in range(1,21):
	if i % 2 == 0:
		even_list.append(i)


even_list = [i for i in range(1,21) if i % 2== 0]
```