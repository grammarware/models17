# Revisiting Visitors for Modular Extension of Executable DSMLs
Manuel Leduc, Thomas Degueule, Benoit Combemale, Tijs van der Storm and Olivier Barais

The *Revisitor* pattern is a language implementation pattern that enables independent extensibility of the syntax and semantics of metamodel-based DSLs, with incremental compilation and without anticipation.
It is inspired by the [Object Algebra](https://dl.acm.org/citation.cfm?id=2367167) design pattern and adapted to the specificities of metamodeling.

On top of the *Revisitor* pattern, we introduce *ALE*, a high-level language for semantics specification of metamodels that compiles to *Revisitors* to support separate compilation of language modules.

*ALE* is tightly integrated with the [Eclipse Modeling Framework](https://www.eclipse.org/modeling/emf/) (EMF) and relies on the Ecore meta-language for the definition of the abstract syntax of DSLs. Operational semantics is defined with *ALE* using an open-class-like mechanism. *ALE* is bundled a set of Eclipse plug-ins.

## Artifacts
- MODELS'17 paper: http://gemoc.org/ale/revisitors/
- ALE Compiler: https://github.com/manuelleduc/ale-compiler/
- ALE Examples & Benchmarks: https://github.com/manuelleduc/ale-compiler-benchmarks/

## Instructions
The repositories mentioned above contain the appropriate installation and usage instructions:

- Installing & using ALE: https://github.com/manuelleduc/ale-compiler/blob/master/README.md
- Running the examples & benchmarks: https://github.com/manuelleduc/ale-compiler-benchmarks/blob/master/README.md

