---
id: vx4antlc9ha06q3g5nwvpz3
title: Args_and_kwargs
desc: ''
updated: 1753264297682
created: 1753264035819
---


index(char)

```bash
def add(*args):
	print(type(args))
	print(args)
	
add(2,3,4,5,6,7,8,9)

- remark - *args return Truple data type
-------------------- 

def concatenate(**kwargs)
	final_string = f"{kwargs['name']} is {kwargs['age']} years old and he lives in {kwargs['city']} , {kwargs['country']}
	return final_string
	
concatenate(name = "ko ko " , age = 23 , city = "yangon", country ="myanmar")


------------------

def my_func(a,b, *args , **kwargs):
	print(a)
	print(b)
	print(args)
	print(kwargs)
	
my_func(3,4,5,6,7,8, name ="aung aung" , age = '12' )

```


