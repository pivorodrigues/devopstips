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

- **How to sort a Python dict by value**

  ```
    # How to sort a Python dict by value
    # (== get a representation sorted by value)

    >>> xs = {'a': 4, 'b': 3, 'c': 2, 'd': 1}

    >>> sorted(xs.items(), key=lambda x: x[1])
    [('d', 1), ('c', 2), ('b', 3), ('a', 4)]

    # Or:

    >>> import operator
    >>> sorted(xs.items(), key=operator.itemgetter(1))
    [('d', 1), ('c', 2), ('b', 3), ('a', 4)]
  ```    

#

- **The get() method on Python dicts and its "default" arg**

  ```
    # The get() method on dicts
    # and its "default" argument

    name_for_userid = {
        382: "Alice",
        590: "Bob",
        951: "Dilbert",
    }

    def greeting(userid):
        return "Hi %s!" % name_for_userid.get(userid, "there")
  ```

  ```
    >>> greeting(382)
    "Hi Alice!"

    >>> greeting(333333)
    "Hi there!"
  ```

#
