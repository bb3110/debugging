<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
# Introduction to debugging

## Olav Vahtras

### Computational Python

---

layout: false


### The pdb module

    
```
>>> import pdb
>>> dir(pdb)
['Pdb', 'Repr', 'Restart', 'TESTCMD', '__all__', '__builtins__', '__doc__', '__file__', '__name__', '__package__', '_repr', '_saferepr', 'bdb', 'cmd', 'find_function', 'help', 'line_prefix', 'linecache', 'main', 'os', 'pm', 'post_mortem', 'pprint', 're', 'run', 'runcall', 'runctx', 'runeval', 'set_trace', 'sys', 'test', 'traceback']

```

--

* Execute a string statment

```
>>> pdb.run('print "Hello world!"')
> <string>(1)<module>()
(Pdb)


```
--

```
    (Pdb) continue
    Hello world!
```

--

* Evaluate a string expression

```
>>> pdb.runeval('1 > 0')
> <string>(1)<module>()
(Pdb)
```
--

```
(Pdb) continue
True
```

---

In larger code insert a break point

```
>>> def sum(a, b):
...    pdb.set_trace()
...    c  = a - b
...    return c
```

---


### pdb commands

Some of the most used commands are common ``gdb``

* step (s) : execute the next line (for function calls step into that function)
* next (n) : execute the next line (for function calls complete the function all and stop at the next line of current function)
* break (b): set break point
* continue (c): continue execution

---


```
>>> (Pdb) help
Documented commands (type help <topic>):
========================================
EOF    bt         cont      enable  jump  pp       run      unt   
a      c          continue  exit    l     q        s        until 
alias  cl         d         h       list  quit     step     up    
args   clear      debug     help    n     r        tbreak   w     
b      commands   disable   ignore  next  restart  u        whatis
break  condition  down      j       p     return   unalias  where 
...
```
     
See http://docs.python.org/2/library/pdb.html for more docs

---

The pydb debugger
-----------------
* This is built upon the pdb module 
* includes a large part of the ``gdb`` command set
* http://bashdb.sourceforge.net/pydb/

...
---

```
    $ pydb
    (Pydb) help
     Documented commands (type help <topic>):
     ========================================
     EOF    cd         directory    finish   jump  pp       run     source     x
     R      cl         disable      frame    kill  pwd      s       step     
     T      clear      disassemble  h        l     pydoc    save    tbreak   
     alias  commands   display      handle   list  python   set     unalias  
     b      condition  down         help     n     q        shell   undisplay
     break  continue   enable       ignore   next  quit     show    up       
     bt     debug      examine      info     p     restart  signal  whatis   
     c      delete     file         ipython  pdef  return   skip    where    
     
     Miscellaneous help topics:
     ==========================
     exec  retval
``` 

---

Trying out pydb
```
$ pydb bugsum.py
(...bugsum.py:5):  <module>
5 sum(5, 3)
```
--
```
(Pydb) step
--Call level 0 sum(a=5, b=3)
(...bugsum.py:1):  sum
1 def sum(a, b):
(Pydb)
```
--
```
(Pydb) next
(...bugsum.py:2):  sum
2     c = a - b
```
--
```
(Pydb) next
(...bugsum.py:3):  sum
3     return c
(Pydb)
```
--
```
(Pydb) print c
2
(Pydb)
```
---

### Summary

* `pdb`  and `pydb` modules  for debugging
* Useful shortcut: insert the line
```
import pdb; pdb.set_trace()
```
anywhere in your code to get a breakpoint and the run the program as normal




