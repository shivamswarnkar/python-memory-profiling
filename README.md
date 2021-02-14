# Find and Profile Memory Leaks (Python)

# Profile Overall Mem Usage

It'll attach itself to the running process and then plot the overall mem usage overtime, you just have to give it the right pid.
Use it to figure out if memory is increasing overtime.

```
$ pip install psrecord
```

```
$ psrecord pid --plot plot.png
```

```
$ psrecord pid --log activity.txt
```

# Profile explicitly

It'll profile throughout the run of the script, and save detailed call stack at the end as a html or svg file.
Find the file or line number which has largest mem allocation.

```
$ pip install filprofiler
```

```
$ fil-profile run server.py
```

# Profile in script

Use in-built tracemalloc

```
#test.py
import tracemalloc

tracemalloc.start()

# take snapshot
s = tracemalloc.take_snapshot()

# do your stuff

# take current snapshot and compare lines
top_states = tracemalloc.take_snapshot().compare_to(s, 'lineno')

print('\n'.join(map(str, top_states[:5])))
```

# Profile script (specific functions)

Use memory_profiler

First add @profile to target functions

```
$ pip install memory_profiler
```

```
#test.py
from memory_profiler import profile

@profile
def test_func(args):
    pass

# call test func however you want
```

Then run the python script as below

```
$ python -m memory_profiler test.py
```

# Resources & References

- [Fil Profiler Example](https://pythonspeed.com/articles/python-server-memory-leaks/)
- [tracemalloc talk](https://youtu.be/s9kAghWpzoE)
