# Pytricks

A repository filled with (Perl-like and arcane) Python rituals
to do very specific things which I often need to Google or go
onto SO to conjure up.

 - [``__init__`` for namedtuple](#__init__-for-namedtuple)
 - [``__exit__`` template](#__exit__-template)

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
