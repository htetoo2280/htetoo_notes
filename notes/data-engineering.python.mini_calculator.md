---
id: vipd5gfj2qn32b7vthg8w2k
title: calculator
desc: ''
updated: 1753262753688
created: 1753262235536
---

```bash


def add(one , two):
    return one + two

def minus(one , two):
    return one - two

def multiply(one , two):
    return one * two

def divided(one , two):
    return one / two


while True:
    print("input operator")
    print("1 - add")
    print("2 - minus")
    print("3 - multiply")
    print("4 - divided")


    opt_input = input("choose an operator  :  ")
    if opt_input in ("1","2","3","4"):
        first_num = float(input("first_num : "))
        sec_num = float(input("second_num : "))

        if opt_input == "1":
            result = add(first_num , sec_num)
            print(result)

        elif opt_input == "2":
            result = minus(first_num , sec_num)
            print(result)

        elif opt_input == "3":
            result = multiply(first_num , sec_num)
            print (result)

        else:
            result = divided(first_num , sec_num)
            print(result)

        next_cal = input("do you want more Y/N : ").lower()
        if next_cal == 'n':
            break
        

    else:
        print ("not match") 


    
    
```