1. \_\_call\_\_()方法理解
    > The \_\_call_\_ method enables Python programmers to write classes where the instances behave like functions and can be called like a function.
    When the instance is called as a function; if this method is defined, x(arg1, arg2, ...) is a shorthand for x.\_\_call\_\_(arg1, arg2, ...).

    **Example:**
    ```python
    class Example: 
    def __init__(self): 
        print("Instance Created") 
      
    # Defining __call__ method 
    def __call__(self): 
        print("Instance is called via special method") 
  
    # Instance created 
    e = Example() 
  
    # __call__ method will be called 
    e() 
    ```

