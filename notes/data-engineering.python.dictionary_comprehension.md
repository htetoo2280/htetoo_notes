---
id: 9xa5kqtn1biyo9fya21c9mu
title: Dictionary_comprehension
desc: ''
updated: 1753259229793
created: 1753257464217
---

``` bash
range(0,10)
list(range(0,10))
new_list.append()

## list comprehension
lst = [2,3,4,5]
new_lst = [num*2 for num in lst]
print(new_list)

even_list=[]
for i in range(1,21):
	if i % 2 == 0:
		even_list.append(i)


even_list = [i for i in range(1,21) if i % 2== 0]

```

---------------------

```bash
students = {"aung":100 , "Ko":100 , "Paing":150 , "Mya":200}  --- key value pair 

check this for students
for i in students:
	print(i) -- will export keys only(columns checking)

check this for iteam method
for i in students.items():
	print(i)  --- will export as turples

this is normal
students_under120 = {name:mark for (name,mark) in students.items()}
print(students_under120)

if 100 
students_under120 = {name:mark for (name,mark) in students.items() if mark == 100}
print(students_under120)

mark + 20  
students_under120 = {name:mark + 20 for (name,mark) in students.items() if mark == 100}
print(students_under120)

```

---------------------------------------- 

## list to dictionary

```bash
to import random
import random 
names = ["aung","kyaw",Mya","paing"]
students_marks = {name:random.randint(1,100) for name in names}
print(students_marks)

```


