Assigning a variable inside a function makes it local to that function, where as for example using a .append method, the compiler will first check whether there is a local variable with it, once it sees there isn't, it falls back on the global one.

Using the keyword `global` tells the compiler that the following variable within the scope of the function refers to the global module variable.

General rule is that the python compiler will look outwards according to the Local, Enclosing, Global, Built-in (LEGB) rule, except when assignments are made within a scope. When that happens, the name becomes local for that scope. 
```Python
x = 10 
def f(): 
	print(x) # UnboundLocalError, not 10! x = 20
	x = 20
```
Python sees that x = 20 was assigned within the scope of f(), and so x is a local variable within the scope of the function, hence why `print(x)` returns an error.