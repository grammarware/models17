# From Secure Business Process Modeling to Design-Level Security Verification
Qusai Ramadan, Mattia Salnitri, Daniel Strüber, Jan Jürjens and Paolo Giorgini

In this file, we present the artifact submission for our paper of the same name, to
be presented at the MoDELS conference 2017 in Austin, TX. Our submission includes
the model transformation from SecBPMN2 to UMLsec models as well as four examples
models from the Air Traffic Management System case study. We explain the process of
using the transformation, and the verification of the generated UMLsec models using
the CARiSMA tool.

# Resources

* **MODELS'17 paper (preprint version):** https://github.com/grammarware/models17/blob/master/ramadan/From%20Secure%20Business%20Process%20Modeling.pdf
* **Artifact paper:** https://github.com/grammarware/models17/blob/master/ramadan/Artifact_Evaluation_Paper.pdf
* **Artifact: Model Transformation Project package:** https://github.com/grammarware/models17/blob/master/ramadan/myexample.zip
* **A mirror of the CARiSMA update site:** https://github.com/grammarware/models17/blob/master/ramadan/CARiSMA.zip
* **A mirror of the Henshin update site:** https://github.com/grammarware/models17/blob/master/ramadan/org.eclipse.emf.henshin.sdk_1.5.0.zip

# Artifact contents

The Eclipse project package *myexample.zip* has the following contents:

* *src/my.example* directory:
  * *Externalservices1.bpmn, Externalservices2.bpmn, Flightplan.bpmn, Landing.bpmn:* Input models from the ATM case study
  * *example1.bpmn:* Small input model for testing purposes
  * *\*.henshin files:* Henshin modules implementing the transformation
  * *BpmnToUml.java:* Java class for executing the transformation via orchestration of Henshin modules
  * *BpmnToUmlMetricsPrinter.java:* Java class for computing metric values for input and output models
  
* *Testing* directory: Additional test input models 



# Usage 
The uploaded [myexample.zip](https://github.com/grammarware/models17/blob/master/ramadan/myexample.zip) file includes all the required artifacts for transforming SecBPMN2 to UMLsec models.
## Prerequisite 
We recommend using [Eclipse Neon, Modeling Tools distribution](https://www.eclipse.org/downloads/packages/eclipse-modeling-tools/neonr), with
an installed nightly build of [Henshin](https://www.eclipse.org/henshin/) and [CARiSMA](https://rgse.uni-koblenz.de/carisma/). These plug-ins can be installed either using  online update sites, or the mirrored update sites provided as part of the artifact. 
**From the CARiSMA update site, please only install the main features (BPMN2 and UML2 support).**

* **Installation from online update sites**: In Eclipse, do *Help → Install New Software...*. Use the following online update
sites: http://carisma.umlsec.de/updatesite for CARiSMA, and  http://download.eclipse.org/modeling/emft/henshin/updates/release for Henshin. 

* **Installation from mirrors**: Download the mirrored update sites (i.e. CARiSMA.zip and org.eclipse.emf.henshin.sdk_1.5.0.zip) to your computer → install both of them in Eclipse, using *Help → Install New Software... → Add → Archive*.


## Performing the transformation. 
To execute the transformation from SecBPMN2 to UMLsec models, please follow the following instruction. 
* Import our project package to your local Eclipse workspace.
* Right click on the main class *"src/my.example/BpmnToUml.java"* → *Run As JUnit Plug-in Test*. By default, our transformation takes as input the *example1.bpmn* file. To change the input file, first copy the name of one of the BPMN files
that are provided in *myexample → src → my.example* directory. Second, find line 91
in the *BpmnToUml.java* file (**public static final String EXAMPLE = "example1.bpmn";**)  and replace the file name *"example1"* with the name of
the selected BPMN file.
* After running the *BpmnToUml.java* file, you should see console output informing you about
the generation process. The process could take a few minutes, and there might be some warnings/error messages related to the underlying plug-ins. As these do not concern us, we can ignore them. The process is finished when the following line is printed to the console: *Saved result in 'example1-generated-result.uml'.*
* The results of the transformation process (.uml file) will be stored to the project root directory. The name of the UML file is **Transformed_serialized_profile.uml**.

## Performing the verification. 

In this step, we use CARiSMA checks to verify the generated UML models against UMLsec security policies. For this, please follow the following istructions.

* Right click on the *myexample* project in the *Project Explorer view* → New → Other → CARiSMA → Analysis
→ Next → in the dialog select the file that is generated from the last step (i.e.,
Transformed_serialized_profile.uml) and then click finish.
* From the *analysis editor* window click on the *add checks to list* icon → select the check that you
want to perform (e.g., secure links UMLsec check and secure dependency UMLsec
check) then click *RUN*. For RABAC policy, you have to select both *RABACsec: Create
transformation input* and *RABACsec: Use transformation input checks* checks. The former
allows you to select the role that you want to verify his accessibility to the system
operations, while the second return the set of operations that the selected role have an
access to them. More details about the execution of abac checks will provided below. Other information can also be found in the user manual
of CARiSMA. After installing CARiSMA, the manual is available under: *Help →
Help Contents → CARiSMA*.
* The result of the verification is provided in the *Analysis Results view*. One can also
*right click* on the result and select *create a report for the selected analysis*. The report
will be stored to the project root directory.

## More details information about performing CARiSMA checks

In what follows, we walk through the three checks supported by our transformation output: «secure links» (for deployment diagrams), «secure dependency» (for class diagrams), and RABAC (for class diagrams).


### 1. «secure links» UMLsec check

**Purpose:** To check whether the communication links between physical nodes are secure or not with respect to the adversary type and the data communicated across them. To perform this check on the generated UML file from the earlier steps (i.e., Transformed_serialized_profile.uml), please mind  the following instructions: 

* In the *analysis editor* window, click on the *add checks to list* icon → select the *secure links UMLsec check* and then click *RUN*. 

### 2. «secure dependency» UMLsec check

**Purpose:** To check whether the dependencies between objects or subsystems respect the security requirements on the data  communicated across them. To perform this check on the generated UML file from the earlier steps (i.e., Transformed_serialized_profile.uml), please follow the following instructions:

* From the *analysis editor* window click on the *add checks to list* icon → select the *secure dependency UMLsec check* → click OK and then click *RUN*. 


### 3. RABAC (Role Attribute-based Access Control)

**Purpose:** To check the access rights of each role and the access constraints assigned to specific operations based on predefined attributes. UMLsec  implements  the RABAC  access  control  model  via  the  policy *«abac»*,  which uses  two  tags  called *{role}* and *{right}* to  assign  roles  to subjects and rights to roles, respectively. Operations in need of an access restriction can be annotated with the *«abacRequire»* stereotype  along  with  its  associated *{right}* tag. 

**Prerequisite:** In our transformation, we can automatically assign *roles* to subjects and the *rights* that are needed for restricting the access for some operation. Since our transformation does not allow to automatically specify all the required information for excuting the RABAC check, some information still needs to be inserted manually: One needs to  manually assign  rights to roles, based on the following instructionss: 

* Right click on the generated UML file from the last step (i.e., Transformed_serialized_profile.uml) → open with → UML Model Editor.
* Click on platform:/resource/myexample/Transformed_serialized_profile.uml → open the model → select the *RABAC* class. 
* In the *propertie*s view, assign a value to the *"right"* property. The value should have the following format: **{(role_name,right)}**. For instance, *{(Airplane, Modify_Flight plan)}*,  means that the Airplan has the right to modify a flight plan data. Multiple rights can be given to the same role as follows: *{(Airplane, Modify_Flight planRead_Flight plan)}*. This means that the Ai plane has the right to both read and modify the flight plan. In what follows, we will assume that   *{(Airplane, Modify_Flight planRead_Flight plan)}* is the specified as a value for the *"right"* property.

* Save the changes you made on the models.
** perform RABAC checks:** To perform this check on the generated UML file (i.e., Transformed_serialized_profile.uml) from the last steps, please mind the following instructions:

* In the *analysis editor* window, select both the *RABACsec: Create transformation input* and *RABACsec: Use transformation input checks* checks and click OK. 
* In the checks list, you will see the selected RABAC checks. To perform the checks, first unselect the selected checks, only select the *RABACsec: Create transformation input* and  click *RUN*.
* Save the configration file *"rabac_configuration.xml"* into *myexample* directory.
* In the pop-up window *"RABACsec transformation input"*, first click on the droplist of the users and select *"subject"*.
* From the droplist of the roles, we can select a role for which we want to view the accessible operations. For example, select *Airplane*.
* The *Active* checkbox allows you to identify whether the selected role is active or not. Please tick the checkbox.
* Put the cursor inside the the *Value* textbox and press *enter* to save the changes. This textbox can be used to specify some attributes for the selected role. However, this not part of our work. Therefore, please leave the textbox empty.
* Click *Save* and close the window. 

**Hint:** Please press enter in the textbox to save the changes, ignoring the *Save* buttom. This because of a bug in the  implementation of the check.

* In  the *analysis editor* window, uncheck the last performed check (*RABACsec: Create transformation input*), only select *RABACsec: Use transformation input checks* check and  click *Run*.

* Press *OK* in the pop-up window and  select the generated configration file from the last step (i.e., "rabac_configuration.xml") and  click *Open*.
* The result of the verification is provided in the *Analysis Results view*.


To generate the report text file for the generated checks, you can *right click* on the result and select *create a report for the selected analysis*. The report
will be stored to the *myexample* directory.  In our example, the  output resut for the RABAC check  will show that the selected *Airplane* role has an access to *Notify local authority* operation. 

