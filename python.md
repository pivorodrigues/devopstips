# Python Language
_(Based on Data Science Academy Course)_

### Numbers and Operations

- **Number types: int and float**

  - We can use the function **type()** to discover what type of number we are using.

    _Example:_

    ```
      a = 5
      type(a)

      <class 'int'>
    ```

  - We can convert types of numbers.

    _Example:_

    ```
      a = 5
      float(a)
      5.0

      a = 5.5
      int(a)
      5
    ```

  **OBS:** [_Python Built-in Functions_](https://docs.python.org/3.3/library/functions.html)

- **Number operations**

#

### Conditionals and Loops

- **Range: function range()**

  **Sintax:**

    `range([start],[stop],[step])`

  **Examples:**

    ```
      for i in range(5, 101, 2):
          print(i)
    ```

    ```
      list = ["strawberry", "banana", "pineapple", "grape"]
      list_size = len(list)
      for i in range(0, list_size):
          print(list[i])
    ```      
