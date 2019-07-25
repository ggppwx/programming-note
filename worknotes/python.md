# python notes

## calling sequence 
```python
f = Foo()

# first 
__call__()

# then __call__ invokes 
__new__() # when instantiation 
__init__()
```


## metaclass
why metaclass? to customize **class** itself. (not instance )

metaclass is a class whose instance is a class.

`type` is the metaclass from which all new-style classes are derived. 

```python
Foo = type('Foo', (), {}) # this is a class 
Bar = type('Bar', (Foo), dict(attr=100)) # a derived class 

# meta class to modify the true class 
class Meta(type):
    def __init__(cls, name, bases, dict):
        cls.attr = 100

class Y(metaclass=Meta)
```

can be achieved by **class decorator**



## singleton 
they are no usually thread-safe 

`super` to get the parenet class 

