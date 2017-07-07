# From Secure Business Process Modeling to Design-Level Security Verification
Qusai Ramadan, Mattia Salnitri, Daniel Strüber, Jan Jürjens and Paolo Giorgini

# Usage 
The uploaded myexample.zip file includes all the required artifacts for transforming SecBPMN2 to UMLsec models.
## Prerequisite 
We recommend using [Eclipse Neon, Modeling Tools distribution](https://www.eclipse.org/downloads/packages/eclipse-modeling-tools/neonr), with
an installed nightly build of Henshin and[ CARiSMA. These softwares plug-ins can be[
installed on your Eclipse (Help –>Install New Software...) from the the follwing update
sites: for CARiSMA use (http://carisma.umlsec.de/updatesite), while for Henshin one
can use (http://download.eclipse.org/modeling/emft/henshin/updates/release).
Performing the transformation. To execute the transformation from SecBPMN2
to UMLsec models, please follow the following instruction. More details can also be
found in the Read Me file.
– Import our project package to your local Eclipse workspace.
– Right click on the main class BpmnToUml.java–> Run As JUnit Plug-in Test to
perform the transformation. By default, our transformation takes as input the example1.
bpmn. To change the input file, first copy the name of one of the BPMN files
that are provided in myexample –> src –> my.example directory. Second find the following
line of code (public static final String EXAMPLE = "example1.bpmn";)
in the BpmnToUml.java file and replace the file name "example1" with the name of
the selected BPMN file.
– After starting the runner class, you should see console output informing you about
the generation process.
– The results of the transformation process (.uml file) will be stored to the myexample
directory. The name of the UML file is Transformed_serialized_profile.
Performing the verification. In this step, we use CARiSMA checks to verify the
generated UML models against UMLsec security policies.
– Right click in the Project Explorer view –> New –> Other –> CARiSMA –> Analysis
–> Next -> in the dialog select the file that is generated from the last step (i.e.,
Transformed_serialized_profile.uml) and then click finish.
– From the dialog, click on add checks to the list icon –> select the check that you
want to perform (e.g., secure links UMLsec check and secure dependency UMLsec
check) then click run. For abac policy, you have to select both RABACsec: Create
transformation input and RABACsec: Use transformation input checks. The former
allows you to select the role that you want to verify his accessibility to the system
operations. While the second return the set of operations that the selected role can
access to them. More details about the execution of CARiSMA checks are provided
in the Read Me file. Other information can also be found in the user manual
of CARiSMA. After installing CARiSMA, the manual is available under:Help –>
Help Contents –> CARiSMA.
– The result of the verification is provided in the Analysis Results view. One can also
right click on the result and select create a report for selected analysis. The report
will be stored to the myexample directory.
