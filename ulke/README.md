# Partial Evaluation of OCL Expressions
Bastian Ulke, Friedrich Steimann and Ralf Lämmel
(latest revision of the accepted paper available at http://www.feu.de/ps/prjs/models2017.pdf)

Abstract (taken from the paper) -- In the academic literature, many uses of the Object Constraint Language (OCL) have been proposed. By contrast, the utilization of OCL in contemporary modelling tools lags behind, suggesting that leverage of OCL remains limited in practice. We consider this undeserved, and present a scheme for partially evaluating OCL expressions that allows one to capitalize on given OCL specifications for a wide array of purposes using a single implementation: a partial evaluator of OCL.


In this context, our artifact delivers the following contributions:
1. it presents a Java-based partial evaluator for OCL invariants. The partial evaluator evaluates OCL subexpressions where their value is fix and translates them to a constraint on variables where they are not (the genrated constraints can be solved by a constraint solver to find value assignments satisfying the invariants, thus repairing or completing a model instance; refer to section II for more details).
2. The artifact comprises a text-based user interface to illustrate the constraint generation based on a user-specified set of dynamic and fix properties.
3. The same interface can be used to reproduce the results of the implementation evaluation (please refer to section IX of our paper for further details).
4. Our artifact also publishes the models and OCL invariants that were used for the evaluation.


The artifact consists consists of three parts:

1. The metamodel for Java/JPA programs and 14 instances, constructed from Open Source projects, as well as the 77 OCL expressions reflecting JPA's rules of well-formedness.

	(URL: https://figshare.com/s/424885f29178e33c4fd6)

2. A Java SE-based setup of our Java-based OCL partial evaluator. This application can be used to reproduce evaluation results presented in our paper and to get an impression of the complexity reduction achieved by partially evaluating OCL expressions.

	(URL: https://figshare.com/s/50d816054286e2086a85)
	
3. A virtual machine, comprising a preconfigured Eclipse workspace to inspect the implementation of our partial evaluator for OCL. (Depending on your system configuration, you may want to ensure that the VM is set up to run an "Ubuntu (64 bit)" operating system.)

	(URL: https://figshare.com/s/0d0ec7567d12ac45c253)
	

Parts (2) and (3) contain own README files with further details on their usage.

