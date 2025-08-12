---
id: mhe3xu2byzhjcftnymr7quy
title: Break_continue_and_pass
desc: ''
updated: 1753260475959
created: 1753260351767
---


```bash
- break stop the whole looping
lst = [1,2,3,4,5,6,7,8,9]
for num in lst:
	if num != 5:
		print(f"Valid Number => {num}")
	else:
		break #stop the whole looping
	-- result will be 1,2,3,4


- continue skip the below steps and relooping
lst = [1,2,3,4,5,6,7,8,9]
for num in lst:
	if num != 5:
		print(f"Valid Number => {num}")
	else:
		continue # skip the below and relooping
	-- result will be 1,2,3,4,   ,6,7,8,9
	
-------------- 

-- pass

- create function and call (pass) will not error
- use when incomplete function

def func():
    pass

func() -- this will not be error

```



		
	