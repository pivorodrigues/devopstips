# PyTricks

_Based on Real Python's mailist_

#

- **Merging two dicts in Python 3.5+ with a single expression**

  ```
    # How to merge two dictionaries
    # in Python 3.5+

    >>> x = {'a': 1, 'b': 2}
    >>> y = {'b': 3, 'c': 4}

    >>> z = {**x, **y}

    >>> z
    {'c': 4, 'a': 1, 'b': 3}

    # In Python 2.x you could
    # use this:
    >>> z = dict(x, **y)
    >>> z
    {'a': 1, 'c': 4, 'b': 3}

    # In these examples, Python merges dictionary keys
    # in the order listed in the expression, overwriting
    # duplicates from left to right.
  ```

  See at: https://www.youtube.com/watch?v=Duexw08KaC8

#

- **Different ways to test multiple flags at once in Python**

  ```
    # Different ways to test multiple
    # flags at once in Python
    x, y, z = 0, 1, 0

    if x == 1 or y == 1 or z == 1:
      print('passed')

    if 1 in (x, y, z):
      print('passed')

    # These only test for truthiness:
    if x or y or z:
      print('passed')

    if any((x, y, z)):
      print('passed')
  ```
#    
