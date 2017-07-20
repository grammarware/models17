# From Secure Business Process Modeling to Design-Level Security Verification
Qusai Ramadan, Mattia Salnitri, Daniel Strüber, Jan Jürjens and Paolo Giorgini

In this file, we present the artifact submission for our paper of the same name, to
be presented at the MoDELS conference 2017 in Austin, TX. Our submission includes
the model transformation from SecBPMN2 to UMLsec models as well as four examples
models from the Air Traffic Management System case study. We explain the process of
using the transformation, and the verification of the generated UMLsec models using
the CARiSMA tool.

# Resources

* **MODELS'17 paper (preprint version):** https://figshare.com/s/2a741558cb1381db8dd6
* **Artifact paper:** https://figshare.com/s/69de2308c85dfc31d9a2
* **Artifact: Project package:** https://figshare.com/s/b292824ca98f2185a949
* **Artifact: A mirror of the CARiSMA update site:** https://figshare.com/s/dc79bf8d4eb451ccca2f
* **Artifact: A mirror of the Henshin update site:** https://figshare.com/s/a922f57fd14c853e313f
* **Artifact: Air Traffic Management Case Study SecBPMN2 models:** https://figshare.com/s/051baa54ee849eca8d4e
* **Artifact: Mirrors of the STS-tool current versions:** https://figshare.com/s/b322d002077d99577949

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
The uploaded [myexample.zip](https://figshare.com/s/b292824ca98f2185a949) file includes all the required artifacts for transforming SecBPMN2 to UMLsec models.
## Prerequisite 
We recommend using [Eclipse Neon, Modeling Tools distribution](https://www.eclipse.org/downloads/packages/eclipse-modeling-tools/neonr), with
installed [Henshin](https://www.eclipse.org/henshin/) and [CARiSMA](https://rgse.uni-koblenz.de/carisma/) plug-ins. These plug-ins can be installed either using  online update sites, or the mirrored update sites provided as part of the artifact. 
**From the CARiSMA update site, please only install the main features (BPMN2 and UML2 support).**

* **Installation from online update sites**: In Eclipse, do *Help → Install New Software...*. Use the following online update
sites: http://carisma.umlsec.de/updatesite for CARiSMA, and  http://download.eclipse.org/modeling/emft/henshin/updates/release for Henshin. 

* **Installation from mirrors**: Download the mirrored update sites (i.e. [CARiSMA.zip](https://figshare.com/s/dc79bf8d4eb451ccca2f) and [org.eclipse.emf.henshin.sdk_1.5.0.zip](https://figshare.com/s/a922f57fd14c853e313f)) to your computer → install both of them in Eclipse, using *Help → Install New Software... → Add → Archive*.


## Performing the transformation. 
To execute the transformation from SecBPMN2 to UMLsec models, please follow the following instruction. 
* Import our project package to your local Eclipse workspace.
* Right click on the main class *"src/my.example/BpmnToUml.java"* → *Run As JUnit Plug-in Test*. By default, our transformation takes as input the *example1.bpmn* file. To change the input file, first copy the name of one of the BPMN files
that are provided in *myexample → src → my.example* directory. Second, find line 91
in the *BpmnToUml.java* file (**public static final String EXAMPLE = "example1.bpmn";**)  and replace the file name *"example1"* with the name of
the selected BPMN file. ** Please note that you cannot directly view or modify these bpmn models from you Eclipse. For viewing and modifying the bpmn models please look into the last section of this README file *viewing and modifying the SecBPMN2 models* **
* After running the *BpmnToUml.java* file, you should see console output informing you about
the generation process. The process could take a few minutes, and there might be some warnings/error messages related to the underlying plug-ins. As these do not concern us, we can ignore them. The process is finished when the following line is printed to the console: *Saved result in 'example1-generated-result.uml'.* The name of the .uml file in this line is  the name of the selected .bpmn  file as input to our transformation folowed by *-generated-result.uml*.
* The results of the transformation process are three files which will be stored to the *myexample/src/my.example* directory: 
   * The first file contains the generated UMLsec model. The name of this file is the name of the selected .bpmn file as input to our transformation followed by *-generated-result.uml* (e.g., example1-generated-result.uml). 
   * The second file contains the generated trace model which links the SecBPMN2 and UMLsec models. The name of this file is the name of the selected .bpmn file followed by *-generated-result-trace.xmi* (e.g., example1-generated-result-trace.xmi). 
   * The third file contains the UMLsec operations that have an access restrections together with rights the should be assigned to the roles to grant them an access for these operations. The name of this file is the name of the selected .bpmn file followed by *-generated-result-rights.txt* (e.g., example1-generated-result-rights.txt). 

## Performing the verification. 

In this step, we use CARiSMA checks to verify the generated UML models against UMLsec security policies. For this, please follow the following istructions.

* Right click on the *myexample* project in the *Project Explorer view* → New → Other → CARiSMA → Analysis
→ Next → in the dialog select the file that is generated from the last step (e.g.,
example1-generated-result.uml) and then click finish.
* From the *analysis editor* window click on the *add checks to list* icon → select the check that you
want to perform (e.g., secure links UMLsec check and secure dependency UMLsec
check) then click *RUN*. 
* For RABAC policy, you have to select both *RABACsec: Create
transformation input* and *RABACsec: Use transformation input checks* checks. The former
allows you to select the role that you want to verify his accessibility to the system
operations, while the second return the set of operations that the selected role have an
access to them. 
* The result of the verification is provided in the *Analysis Results view*. One can also
*right click* on the result and select *create a report for the selected analysis*. The report
will be stored to the project root directory. ** Please note that all the checks should pass except for RABAC check which depends on rights that the user would like to assign to each role during berforming *RABACsec: Use transformation input checks* **.

* More details about the execution of abac checks will provided below. Other information can also be found in the user manual
of CARiSMA. After installing CARiSMA, the manual is available under: *Help →
Help Contents → CARiSMA*.

## More details information about performing CARiSMA checks

In what follows, we walk through the three checks supported by our transformation output: «secure links» (for deployment diagrams), «secure dependency» (for class diagrams), and RABAC (for class diagrams).


### 1. «secure links» UMLsec check

**Purpose:** To check whether the communication links between physical nodes are secure or not with respect to the adversary type and the data communicated across them. To perform this check on the generated UML file from the earlier steps (e.g., example1-generated-result.uml), please mind  the following instructions: 

* In the *analysis editor* window, click on the *add checks to list* icon → select the *secure links UMLsec check* and then click *RUN*. 

### 2. «secure dependency» UMLsec check

**Purpose:** To check whether the dependencies between objects or subsystems respect the security requirements on the data  communicated across them. To perform this check on the generated UML file from the earlier steps (e.g., example1-generated-result.uml), please follow the following instructions:

* From the *analysis editor* window click on the *add checks to list* icon → select the *secure dependency UMLsec check* → click OK and then click *RUN*. 


### 3. RABAC (Role Attribute-based Access Control)

**Purpose:** To check the access rights of each role and the access constraints assigned to specific operations based on predefined attributes. UMLsec  implements  the RABAC  access  control  model  via  the  policy *«abac»*,  which uses  two  tags  called *{role}* and *{right}* to  assign  roles  to subjects and rights to roles, respectively. Operations in need of an access restriction can be annotated with the *«abacRequire»* stereotype  along  with  its  associated *{right}* tag. 

**Prerequisite:** In our transformation, we can automatically assign *roles* to subjects and the *rights* that are needed for restricting the access for some operation. Since our transformation does not allow to automatically specify all the required information for excuting the RABAC check, some information still needs to be inserted manually: One needs to  manually assign  rights to roles, based on the following instructionss: 

* Right click on the generated UML file from the last step (e.g., example1-generated-result.uml) → open with → UML Model Editor.
* Click on platform:/resource/myexample/example1-generated-result.uml → open the model → select the *RABAC* class. 
* In the *properties* view, assign a value to the *"right"* property. The value should have the following format: **{(role_name,right)}**. For instance, *{(Airplane,Modify_Flight plan)}*,  means that the Airplan has the right to modify a flight plan data. Multiple rights can be given to the same role as follows: *{(Airplane,Modify_Flight planRead_Flight plan)}*. This means that the Ai plane has the right to both read and modify the flight plan. 
* One can also get benifits from the generated *example1-generated-result-rights.txt* file that contains all the operations that have an access restraction together with the rights that should be asigned to the system roles to grant them an access to these operations.  In what follows, we will assume that   *{(Airplane,Modify_Flight planRead_Flight plan)}* is the specified as a value for the *"right"* property. ** Please a void whitespaces in your entries, otherwise a matching cannot be found and the check will fail**.

* Save the changes you made on the models.
** perform RABAC checks:** To perform this check on the generated UML file (i.e., Transformed_serialized_profile.uml) from the last steps, please mind the following instructions:

* In the *analysis editor* window, select both the *RABACsec: Create transformation input* and *RABACsec: Use transformation input checks* checks and click OK. 
* In the checks list, you will see the selected RABAC checks. To perform the checks, first unselect the selected checks, only select the *RABACsec: Create transformation input* and  click *RUN*.
* Save the configration file *"rabac_configuration.xml"* into *myexample/src/my.example* directory.
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
will be stored to the *myexample/src/my.example* directory.  In our example, the  output resut for the RABAC check  will show that the selected *Airplane* role has access to *Notify local authority* operation. 

## Viewing and Modifying the SecBPMN2 Models. 
The bpmn models that are provided in *my.example* directory represnts a SecBPMN2 models for our *Air Traffic Management System* case study. Please note that you can not open or modify these models directly from your Eclipse. These models are designed by using the Socio-Technical-System (STS) tool. To view and modify these bpmn models please follow the instructions:
* Install the STS tools from (http://www.sts-tool.eu/) or from the mirrored files of the current STS-version provided as part of the artifacts (available from [here](https://figshare.com/s/b322d002077d99577949)).
* Download the *projects.exp* file from (https://figshare.com/s/051baa54ee849eca8d4e) to your desktop. This file is automatically generated from the STS tool and it contains all the SecBPMN2 models of our case study. 
* To view and modify the models in this file you need to import it into the STS:
   * In the STS tool, do *File→ Import → project → next → select the "projects.exp" file from your desktop. 

* In case you want to insert a new designed SecBPMN2 model or a modefied version of the provied SecBPMN2 models into our transformations approach, please:
   * First, from the workspace of the STS tool please finde the SecBPMN2 model file that you want to transform. 
   * Second, simply copy and paste the file into the *my.example* directory. 
   * Third, since our approach take an inpt a (.bpmn) files, please right click on the inserted file  → rename → change the file   extension to bpmn.
   
## Viewing the generated UMLsec model. 
To create a Papyrus UML diagram initialized with the contents of a given .uml model file (e.g., example1-generated-result.uml), please follwo the below instructions:
* create a new Papyrus model by right-clicking the UML model (e.g., example1-generated-result.uml)  → New → Other → select Papyrus Model → Select UML  → save the model to the root directory of our project (i.e., myexample) → Finish. 
* From the Repair Streotypes and some profiles have changed pop-up windows press OK. After that, the .di and .notation files are created. By following the previous instructions, the required files to work with the UML model in Papyrus can be initialized. 
* Now make sure that you are working on the Papyrus modeling perspective  → open the created Papyrus model → create view  → select the root element of our UML model → select the desired type of UML diagrams that you want to create  → enter a name to the diagram. **Please note that our .uml file only contains elements related to the Deployment and Class diagrams**
* After opening the created diagram you will see nothing but a blank window. This because in general .uml file has no information regarding any diagram. All you have is the model elements, but no diagrams. Therefore, you have to create the diagrams manually by dragging and dropping the model elements to the desired diagram view (e.g., class ). To do so, make sure that you are working in Papyrus modeling perspective view and the *Model Explorer* view is visible. 
Since one can see that dragging and dropping the UML elements to the diagram view manually is a time and efforts consuming, we can suggest another way to perform this task. 
* After creating the desired UML diagram, select Diagram from the menu bar of your Eclipse  → Filters  → Synchronized with Model. Then all the UML classifiers elements will be automatically inserted to your diagram. Personally speaking, this suggestion is useless since you need to remove all the classifiers that are not related to your diagram. For example, if you want to create a class diagram, by following the last suggestion not only the classes will be inserted into your class diagram view but also the UML nodes and artifacts which are part of our deployment diagram. Moreover, you still need to drag and drop the missing details such as the operations, dependencies, and associations manually from the Model explorer view. **For further discussion about this issue, please see https://www.eclipse.org/forums/index.php/t/1071157/.** 

## Computing the metric values for input and output models

The Eclipse project package *myexample.zip* has a *BpmnToUmlMetricsPrinter.java* Java class for computing the metric values for input and output models (i.e., SecBPMN2 and UMLsec models). To run the metrics printer, please follow the following instructions:
* First, all example BPMN models (i.e., "example1.bpmn","Flightplan.bpmn","Landing.bpmn","Externalservices1.bpmn", and "Externalservices2.bpmn") have to be transformed.
* Right click on the *BpmnToUmlMetricsPrinter.java* Java class  → Run As → Java Application.  There might be some warnings/error messages related to the underlying plug-ins.
* The result is a console output shows the models and thier metrics values. 
