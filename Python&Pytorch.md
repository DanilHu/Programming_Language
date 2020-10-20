# Python语法
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
2. Python装饰器的
    为了在原的有已经写好的代码中，增加新的功能，而不改变函数本身的逻辑，可以使用python中的装饰器
    > 
    ```python
    def foo():
        print('i am foo')
    ```
    新的需求是希望可以记录函数的执行日志，于是可以添加
    ```python
    def foo():
        print('i am foo')
        logging.info("foo is running")
    ```
    如果这个时候bar(),bar2()也有同样的需求，按照上面的方法改的话，会造成大量重复的代码。
    ```python
    def use_logging(func):
        def wrapper(*args, **kwargs):
            logging.warn("%s is running" % func.__name__)
            return func(*args)
        return wrapper
    @use_logging
    def bar():
        print("i am foo")
    这样执行bar()函数的时候相当于执行了：
    bar = use_logging(bar)
    bar()
    ```
# Pytorch语法
1. Convert 3d tensor to 4d tensor
    ```python
    x = torch.zeros((4,4,4))   # Create 3D tensor 
    x = x.unsqueeze(0)         # Add dimension as the first axis (1,4,4,4)

    print(x[None].shape)       #  (1,4,4,4)
    print(x[:,None,:,:].shape) #  (4,1,4,4)
    print(x[:,:,None,:].shape) #  (4,4,1,4)
    print(x[:,:,:,None].shape) #  (4,4,4,1)
    ```
