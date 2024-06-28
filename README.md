
# Pointers-in-While-Lang

This repository demonstrates the Extension of wlang with references 

## Overview

This project aims to extend the wlang (While Language) with references. A reference is a variable that is allocated on the heap, which allows for more advanced memory management and data manipulation capabilities. This extension will significantly enhance the functionality of wlang, making it more powerful and versatile for various computational tasks.


## Reference Declaration

We propose to introduce a new syntax for declaring references an example of the same is:
```
  ref x:= new 42
```


## De/Re-referencing

De/Re-referencing a reference to access or modify the value it points to:
```
  y := *x
```


### Potential Abstract Syntax Tree (AST) Modifications to current Codebase:

```
class RefDecl(ASTNode):
    def __init__(self, var_name, var_type):
        self.var_name = var_name
        self.var_type = var_type

class Deref(ASTNode):
    def __init__(self, ref_name):
        self.ref_name = ref_name

# and so on ....
```
#### Potential Parser Modifications to current Codebase

Modify the parser to recognize reference declarations, dereferencing, and assignments

```
class Parser:
  	# Initial code ....
  
    def parse(self, tokens):
        if self.current_token() == 'ref':
            # Parsing logic here

    def parse_ref_decl(self):
        # Parsing logic here

    def parse_deref(self):
        # Parsing logic here

    # and so on ...
```

###  Potential Interpreter Modifications to current Codebase

Extend the interpreter to handle reference operations. We initialize a python dictionary as our heap.

```
class Interpreter:
    def __init__(self):
        self.env = {}
        self.heap = {}

    def eval_ref(self, node):
        # Reference Evaluation Logic

    def eval_ref_decl(self, node):
        # Declaration logic

    def eval_deref(self, node):
        # Evaluate de/re-reference

# and so on...
```

### Example Test Cases:

```
def test_references():
  	# Initializing state
    parser = Parser()
    interpreter = Interpreter()

    # Test reference declaration and dereference
    program = '''
    ref x := new int;
    *x := 5;
    y := *x;
    '''
    ast = parser.parse(program)
    interpreter.eval(ast)
    assert interpreter.env['y'] == 5
```
