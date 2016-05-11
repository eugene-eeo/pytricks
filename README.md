# Pytricks

A repository filled with (Perl-like and arcane) Python rituals
to do very specific things which I often need to Google or go
onto SO to conjure up.

 - [``__init__`` for namedtuple](#__init__-for-namedtuple)
 - [``__exit__`` template](#__exit__-template)
 - [``__hash__`` wtfs](#__hash__-wtfs)
 - [last n items](#last-n-items)

### ``__init__`` for namedtuple

```
Base = namedtuple('Point', ['x', 'y'])

class Point(Base):
    def __new__(cls, x=0, y=0):
        self = super(Point, cls).__new__(cls, x, y)
        return self
```

### ``__exit__`` template

```
def __exit__(self, type, value, traceback):
    return isinstance(value, Exception)
```

### ``__hash__`` wtfs

```
>>> class HashList(object):
  def __init__(self, wrap):
    self.wrap = wrap
  def __eq__(self, other):
    return isinstance(other, HashList) and \
           other.wrap == self.wrap
  def __hash__(self):
    return hash(tuple(self.wrap))

>>> v = [1,2,3]
>>> h = HashList(v)
>>> d = {}
>>> d[h] = 1
>>> d[h]
1
>>> v.append(4)
>>> d[h]
Traceback (...):
  ...
KeyError: ...
>>> h in list(d)
True
>>> h in d
False
>>> v.pop()
>>> d[h]
1
```

### last ``n`` items

```
>>> deque([1,2,3], maxlen=2)
deque([2,3], maxlen=2)
```
