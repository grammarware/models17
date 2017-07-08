# From Secure Business Process Modeling to Design-Level Security Verification
Qusai Ramadan, Mattia Salnitri, Daniel Strüber, Jan Jürjens and Paolo Giorgini

In this file, we present the artifact submission for our paper of the same name, to
be presented at the MoDELS conference 2017 in Austin, TX. Our submission includes
the model transformation from SecBPMN2 to UMLsec models as well as four example
models from the Air Traffic Management System case study. We explain the process of
using the transformation, and the verification of the generated UMLsec models using
the CARiSMA tool.

# Artifacts

* **MODELS'17 paper (preprint version):** https://github.com/grammarware/models17/blob/master/ramadan/From%20Secure%20Business%20Process%20Modeling.pdf
* **Artifact paper:** https://github.com/grammarware/models17/blob/master/ramadan/Artifacts-Evaluation.pdf
* **Our Model Transformation Project package:** https://github.com/grammarware/models17/blob/master/ramadan/myexample.zip

# Usage 
The uploaded myexample.zip file includes all the required artifacts for transforming SecBPMN2 to UMLsec models.
## Prerequisite 
We recommend using [Eclipse Neon, Modeling Tools distribution](https://www.eclipse.org/downloads/packages/eclipse-modeling-tools/neonr), with
an installed nightly build of [Henshin](https://www.eclipse.org/henshin/) and [CARiSMA](https://rgse.uni-koblenz.de/carisma/). These softwares plug-ins can be installed on your Eclipse (Help –>Install New Software...) from the the follwing update
sites: for CARiSMA use (http://carisma.umlsec.de/updatesite), while for Henshin one
can use (http://download.eclipse.org/modeling/emft/henshin/updates/release).

## Performing the transformation. 
To execute the transformation from SecBPMN2 to UMLsec models, please follow the following instruction. 
* Import our project package to your local Eclipse workspace.
* Right click on the main class *"BpmnToUml.java"*–> As *JUnit Plug-in Test*. By default, our transformation takes as input the *example1.bpmn* file. To change the input file, first copy the name of one of the BPMN files
that are provided in *myexample –> src –> my.example* directory. Second, find the following
line of code (**public static final String EXAMPLE = "example1.bpmn";**)
in the *BpmnToUml.java* file and replace the file name *"example1"* with the name of
the selected BPMN file.
* After running the *BpmnToUml.java* file, you should see console output informing you about
the generation process.
– The results of the transformation process (.uml file) will be stored to the *myexample*
directory. The name of the UML file is **Transformed_serialized_profile**.

## Performing the verification. 

In this step, we use CARiSMA checks to verify the generated UML models against UMLsec security policies. For this, please follow the following istructions.

* Right click in the *Project Explorer view* –> New –> Other –> CARiSMA –> Analysis
–> Next -> in the dialog select the file that is generated from the last step (i.e.,
Transformed_serialized_profile.uml) and then click finish.
* From the *analysis editor* window click on the *add checks to list* icon –> select the check that you
want to perform (e.g., secure links UMLsec check and secure dependency UMLsec
check) then click *RUN*. For RABAC policy, you have to select both *RABACsec: Create
transformation input* and *RABACsec: Use transformation input checks* checks. The former
allows you to select the role that you want to verify his accessibility to the system
operations, while the second return the set of operations that the selected role have an
access to them. More details about the execution of abac checks will provided below. Other information can also be found in the user manual
of CARiSMA. After installing CARiSMA, the manual is available under:Help –>
Help Contents –> CARiSMA.
– The result of the verification is provided in the *Analysis Results view*. One can also
*right click* on the result and select *create a report for the selected analysis*. The report
will be stored to the *myexample* directory.

## More details information about performing CARiSMA checks

### First : secure links UMLsec check

**Purpose:** To check whether the communication link between the physical nodes are secure or not with respect to the adversary type. To perform this check on the generated UML file (i.e., Transformed_serialized_profile.uml) from the last steps, please follow the following instructions: 

* From the *analysis editor* window click on the *add checks to list* icon –> select the *secure links UMLsec check* and then click *RUN*. 

### Second: secure dpendency UMLsec check

**Purpose:** To check whether the dependencies between objects or subsystems respect the security requirements on the data that may be communicated across them. To perform this check on the generated UML file (i.e., Transformed_serialized_profile.uml) from the last steps, please follow the following instructions:

* From the *analysis editor* window click on the *add checks to list* icon –> select the *secure dependency UMLsec check* –> click OK and then click *RUN*. 

### Third: RABAC (Role Attribute-based Access Control)

**Purpose:** To check the access rights of each role and the access constrains which can be assigned to specific operation based on predefined attributes. UMLsec  implements  the RABAC  access  control  model  via  the  policy *<<abac>>*,  which uses  two  tags  called *{role}* and *{right}* to  assign  roles  to subjects and rights to roles, respectively. Operations in need of an access restriction can be annotated with the *«abacRequire»* stereotype  along  with  its  associated *{right}* tag. 

**Prerequisite:** In our transformation, we can automatically assign *roles* to subjects and the *rights* that are needed for restricting the access for some operation. since our transformation does not allow to automatically specify all the required information for excuting the RABAC check, some information still need to be inserted manually. In our transformation one still need to assign the rights to the roles manually by following the next instructions: 

* Right click on the generated UML file from the last step (i.e., Transformed_serialized_profile.uml) --> open with --> UML Model Editor.
* Click on platform:/resource/myexample/Transformed_serialized_profile.uml --> open the model --> select RABAC class. 
* From the properties view, assign a value to *"right"* property. The value should have the following format: **{(role_name,right)}**. For instance, *{(Airplane, Modify_Flight plan)}*,  means that the Airplan has the right to modify a flight plan data. In case multiple rights should be given to the same role, one can write it as follows *{(Airplane, Modify_Flight planRead_Flight plan)}*. This means that the Air plane has the right to both read and modify the flight plane. In what follows, we will assume that   *{(Airplane, Modify_Flight planRead_Flight plan)}* is the specified as a value for the *"right"* property.

* Save the changes you made on the models.
** perform RABAC checks:** To perform this check on the generated UML file (i.e., Transformed_serialized_profile.uml) from the last steps, please follow the following instructions:

* From the *analysis editor* window, select both the *RABACsec: Create transformation input* and *RABACsec: Use transformation input checks* checks and then click OK. 
* In the checks list you will see the selected RABAC checks. To perform the checks, first Unselected the selected checks and only select the *RABACsec: Create transformation input* and then click *RUN*.
* Save the configration file *"rabac_configuration.xml"* into *myexample* directory.
* In the pop-up window *"RABACsec transformation input"*, first click on the droplist of the users and select *"subject"*.
* From the droplist of the roles, one can select the role that we want to view to which operations he has an accessbility. For example, select *Airplane*.
* The *Active* checkbox, allows you to identify whether the selected role is active or not. Please, tick the checkbox.
* Put the cursor inside the the *Value* textbox and press *enter* to save the changes. This textbox can be used to specify some attributes for the selected role. However, this not part of our work. Therefore, please leave the textbox empty.
* Click Save and close the window. 

**Hint:** One should press enter in the textbox to save the changes, even there is already a *save* buttom. This because of an exisiting implementation **bug** in check.

* From the *analysis editor* window, uncheck the last perform check (i.e., *RABACsec: Create transformation input*) and only select 
) *RABACsec: Use transformation input checks* check and then click *RUN*.

* Press *OK* on the pop-up window and then select the generated configration file from the last step (i.e., "rabac_configuration.xml") and then click *Open*.
* The result of the verification is provided in the *Analysis Results view*. One can also
*right click* on the result and select *create a report for the selected analysis*. The report
will be stored to the *myexample* directory.  In our example, the  output resut will show that the selected *Airplane* role has an access to *Notify local authority* operation.

