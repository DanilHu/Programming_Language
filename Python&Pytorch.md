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
    - 装饰器是可调用的对象,其参数是另一个函数(被装饰的函数)。 装饰器可能会处理被装饰的函数,然后把它返回,或者将其替换成另一个函数或可调用对象。
    - 装饰器是在模块导入的时候就执行，被装饰的函数或者类只有在真正调用的时候才执行
3. Vscode F12跳转到函数定义后，按`ctrl alt -`跳转回去
4. 实现了`__iter__()`或者`__getitem__()`方法的类都叫做可迭代的对象，iterable就可以被enumerate所迭代，返回下标和值。
    可迭代对象的`__getitem__()`方法指定这个值是什么。E.g.: 值原本是图片，修改`__getitem__()`后，可以让迭代返回值包含上他的地址
    迭代器则指定以什么方式来读：比如每次读的大小，是否需要交换顺序
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
