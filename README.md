# ObjectList

Use methods and method chaining on lists of objects.
Also allowing clean syntax for parallel processing.


## Examples

As an example we define an ObjectList of Path objects.

```python
from objectlist import ObjectList

from pathlib import Path
path_list = [Path('foo/a'), Path('foo/bar/b'), Path('foo/bar/c')]
path_objectlist = ObjectList(path_list)
```

### Getting object attributes and properties
If we would like to get the parents of all paths 

```plaintext
[WindowsPath('foo'), WindowsPath('foo/bar'), WindowsPath('foo/bar')]
```
then using a normal list it is necessary to use a loop:

```python
[p.parent for p in path_list]
```

but using an ObjectList this can be done by
```python
path_objectlist.parent
```

ObjectLists can be easily converted to strings:
```python
path_objectlist.parent.str
```

```plaintext
['foo', 'foo\\bar', 'foo\\bar']
```

### Using object methods and passing arguments
Object methods can also be used

```python
path_objectlist.with_suffix('.txt')
```
```plaintext
[WindowsPath('foo/a.txt'), WindowsPath('foo/bar/b.txt'), WindowsPath('foo/bar/c.txt')]
```

### Using parallel processing

Parallel processing can be activated on existing ObjectLists by using .parallel 

```python
path_objectlist.parallel.with_suffix('.txt')
```

Alternatively parallel processing can be activated when the ObjectList is defined: 

```python
path_objectlist = ObjectList(path_list, 
                             use_parallel_processing=True, 
                             number_of_cores=None,
                             parallel_processing_kwargs=dict(verbose=0), 
                             return_none_if_all_none=True)
```
