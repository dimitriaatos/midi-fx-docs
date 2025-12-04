This is a simple code snippet for checking the execution time of python statements.

This particular example shows the time for removing elements from a set of varying sizes. 

```python
import time


def bench(size: int):

    bag = set()
    for i in range(size):
        bag.add(i)

    # any initialization code goes above
    start = time.process_time()
    # the code we want to time starts below

    for i in range(size):
        bag.remove(i)

    # and it ends here
    end = time.process_time()
    diff = end - start
    print("Size: {}\nTime: {:.10f}".format(size, diff))


# we can see how the running time changes as some variable grows
sizes = [0, 1, 10, 100, 1000, 10000]

for size in sizes:
    bench(size)
```
