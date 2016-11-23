The plugin is still in an experimental state. 
It is not very user friendly (lack of good error messages) and still contains bugs. 
But is useable enough to "translate" a large chunck of standard library. 

Compilation 
===========

The plugin currently works with Coq 8.5pl1.
The easy (and long) way to test the plugin is to follow the following steps:

* Retrieve the plugin and compile it:

        git clone https://github.com/aa755/paramcoq.git
        cd paramcoq 
        make
        sudo make install

To test the plugin:

        cd test-suite
        make ide

It will compile Parametricity.vo which loads the plugin. 
Then, it launches coq-ide with some simple examples. 

Available commands
==================

The default arity is 2. 
The default name is automatically generated when translating a constant (otherwise you need to provide it). 

- Parametricity [Recursive] *ident* [as *name*] [arity *n*].

Declare the translation named *name* from the translation of the constant or the inductive *ident*. 
You can use the recursive option to recursively translate all the constant and inductives which are used by *ident*.

- Parametricity Translation *term* [as *name*] [arity *n*]. 

Define a new constant named *name* obtained by computing the parametricity translation of *term*. 

- Parametricity Module *modulepath*.

Recursively translate everything in a module. 

- Realizer *constant or variable* [as *name*] [arity *n*] := *term*.

Declare *term* to be the translation of a constant. 
Useful to translate terms containing section variables, or axioms. 

Note that all that both translating a term or module may lead to proof obligations (for some fixpoints and opaque terms if you did not import ProofIrrelevence).  

- [Global | Local] Parametricity Tactict := t.

Use the tactic t to solve proof obligations generated by the Parametricity command.
