# Effective python 

## Pythonic thinking ##

### PEP 8 style ###

[PEP 8 style](https://pep8.org/)


### helper function ###


### bytes, str and unicode ###


### how to slice ###


### don't use stride with start/end ###



### list comprehensions ###


### use generator to replace big list comprehension ###




### use *try .. except &#x2026;. else &#x2026; finally* ###




### use *enumerate* instead of *range* ###


### use zip to do parallel iteration ###




## Functions ##




### don't return *None*, throw exception ###




### scope in closure ###




### use generator to replace *list* from function return ###


### Be defensive when iterating over arguents ###
Define a class which includes `__iter__`, pass the object to function 




### Variable positional arguents ###

``` ptyhon
def log(message, *values):
      pass
    
    favorites = [7, 33, 99]
    log('Favorite colors', *favorites)
```



### provide optional behavior with keyword arguments ###

the sequence should be normal, positional, optional arguements 




### Use NONE and docstring to sepecify dynamic default argumetns ###
```python
    def decode(data, default=None):    
      """Load JSON data from a string.
          Args:    
              data: JSON data to decode.
              default: Value to return if decoding fails.
                  Defaults to an empty dictionary.
          """
          if default is None:
              default = {}     
```


### Enforce clarity with keyword-only arguments ###

Add `*` before keyword arguments, then it becomes keyword-only 
```python
    def safe_division_c(number, divisor, *,
                        ignore_overflow=False,
                        ignore_zero_division=False):
```



## Class ##


### Prefer helper clsses over dictionary and tuples ###
Avoid doing dictionary nesting more than one level 
Use `namedtuple` type 
```python
    import collections
    Grade = collections.namedtuple('Grade', ('score', 'weight'))
```


### Accept functions instead of classes ###

Use `lambda` and closure 
Function is first class object 
```python
    class CountMissing(object):
      def __init__(self):
        self.added = 0
    
     def __call__(self): # function
       self.added += 1
       return 0 
    
    counter = CountMissing()  # counter is a function 
    result = defaultdict(couter, current) 
```


### Use `@classmethod` to construct objects generically ###
Map reduce example. 
Add the creation funtion to the base class level 
```python
    class InputData(object):
      def read(self):
        raise NotImplementedError       
      @classmethod
      def generate_inputs(cls, config):
        raise NotImplementedError
    
    
    class Worker(object):
      def map(self):
        raise NotImplementedError
    
      def reduce(self, other)
        raise NotImplementedError
    
      @classmethod
      def create_workers(cls, input_class, config):
        workers = []
        for input_data in input_class.generate_inputs(config):
          workers.append(cls(input_data))  #cls => the sub-class itself 
    
      # LineCountWorker, PathInputData are sub-classes 
      workers = LineCountWorker.create_workers(PathInputData, config)
```

### Initialize parent classes with super ###
Avoid the subclass override the previous subclass, `super()` class only called once 
```python
    class Goodway(TimeFive, PlusTwo):
      def __init__(self, value):
        super(Goodway, self).__init__(value)
        # super().__init__(value) in python 3 
    
    ret = Goodway(5) # order is defined in MRO 
```


### Use Multiple Inheritance only for mix-in utility class ###



## Concurrency ##



### Use `subprocess` to manage child processes ###
-   this makes python a good glue
-   communicate() to run subproceses, that could utilize the CPU 
-   in python3, we could add timeout




### Use threads for blocking I/O. avoid for parallelsim ###
-   GIL, threading may causes program running longer !
-   but if the call is IO bound, for example, system call, threading will help 
```python
class MyThread(Thread):
  def run(self):
    pass
    
    
t = MyThread()
t.start() # run threads
t.join() # wait threads 
```

### Use `lock` to prevent data race 

### Use `Queue` to COORDINATE WORK BETWEEN THREADS
The `Queue` class from `queue` module provides thread-safe approache. 
Need to be aware of problem building pipline. busy waiting, stopping workers, memory explosion. 
```python
in_queue = Queue()
def consumer():
    work = in_queue.get()
    # doing the work
    in_queue.task_done() # eliminate the need for polling done_queue 

Thread(target=consumer).start()

in_queue.put(object())
in_queue.join() # waiting in_queue to finish 
```

### CONSIDER COROUTINES TO RUN MANY FUNCTIONS CONCURRENTLY
- Threads require a lot of memory 
- need special tools like `lock`
- costly to start   

```python
def minimize():
  current = yield
  while True:
    value = yield current # return current 
    current = min(current, value)
    
it = minimize()
next(it)
it.send(10)
it.send(15)
```

### consider `concurrent.futures` for true parallelsim
Because GIL, you may hit performance wall 
we could use `multiprocessing` module
```python
def gcd(pair):
  # some operations
  pass 
  
pool = ProcessPoolExecutor(max_workers=2)
pool.map(gcd, numbers) # gcd(number_pair)

```

## built-in modules


### define function decorators with `functools.wraps` ###
Decorators: run addional code before/after any calls    
Use `wraps` to make the function name unchanged   
```python
    def trace(func):
       @wraps(func)
       def wrapper(*args, **kwargs):
          pass
       return wrapper
```


### consider `contextlib` and `with` statement for reusable try behavior ###

-   with == try/finally block
-   enalbe your objects to `with` using `contextlib`
-   simpler than adding `__enter__` `__exit__`
```python
    @contextmanager
    def debug_logging(level):
       logger.setLevel(level)
       try:
          yield  # which with block execute 
          # yield logger #if we wanna use as 
       finally:
          pass
```



### make `pickle` reliable with `copyreg` ###

-   pickle.dump and pickle.load useful for saving game

    copyreg.pickle(GameState, pickle_game_state)

-   stable import path



### Use `datetime` instead of `TIME` ###
```python
eastern = pytz.timezone('US/Eastern')
nyc_dt = eastern.localize(nyc_dt_native)
utc_dt = pytz.utc.normalize(nyc_dt.astimezone(pytz.utc))
```


### Use built-in algorithm and data structure ###

-   `deque()`
-   `OrderedDict`
-   `defaultdict`
-   `heapq`, `heappush`, `heappop`
-   =bisect<sub>left</sub>(x, 99999) binary serach
-   `itertools`



## collaboration ##
### Write docstrings for class, function, module 
```python
""" Libarary for XXXX
Module level docs 

"""
class Player(ojbect):
  """ class level docs 
  Public attributes:
  - a: what a is ...
  - b: what b is ... 
  """
  
  def find_args():
      """ Function description
      Args:
          a: what a is 
      Returns:
          what the return is       
      """
```

### Use packages to organize modules 
Package structure
```
main.py
mypackage/__init__.py
mypackage/models.py
mypackage/utils.py

```

Exposese some funtions in API
```python
# modules.py
__all__ = ['function']
def fucntion(a):
    pass
```

### Define a root `exception` to insulate callers from API
```python
class Error(Exception):
    """Base class for all exceptions raised by this module"""
    
class SomeRealError(Error):
    pass
    
    
```

### Use virtual environment 
Use `pip3`, Use virtual environment
```
pyvenv /dir/to/project
cd /dir/to/project
source /bin/activate

pip3 install -r requiremets.txt

deactivate
```



## production ##
### Consider module-scoped code to configure deployment environment
```python
# dev_main.py
TESTING = True
```
```python
# prod_main.py
TESTING = False
```
```python
import __main__
if __main__.TESTING:
   # use testing settingss 

```

### Use `repr` strings for debug output 
Always use `repr` version of the object when debug print 
```python
pirnt(repr(a))
print(obj.__dict__)


class Someclass(object):
    def __repr__(self):
        return 'output you want '        
```

### Test everything with unittest
- the only way to have confidence in program is to write tests 
- unit-test for isolated functionality, integration tests for modules that interact 

### Use `pdb` to debug
Add pdb to the code 
```python
def complex_func():
   import pdb; pdb.set_trace() # this is like set break point 
```


### profile before optimizing 
Run `cProfile` module 
```python
profiler = Profile()
profiler.runcall(test)


stats = Stats(profiler)
stats.print_stats()

stats.print_callers()

```


### Use `tracemalloc` to understand memory usage
```python
time1 = tracemalloc.take_snapshot()
.....
time2 = tracemalloc.take_snapshot()
stats = time2.compare_to(time1, 'lineno')

```
