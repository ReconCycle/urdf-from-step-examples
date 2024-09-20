# STEP FILE CREATION

Creation of URDF from step file with program [urdf_from_step](https://github.com/ReconCycle/urdf_from_step) is possible by adding properly named parts representing joints coordinates systems (right) to the robot shape CAD file (left). The addition of joint definitions is possible in any CAD software. Definitions can be added to the robot shape in CAD program-specific native format or to the robot shape already in step file format. For this example, we used Fusion 360 as a CAD program.

<img src="./figures/robot_arm_cad.PNG" 
     height="300"   align="center" >  <img src="./figures/robot_arm_cad_with_cs.PNG" 
     height="300"   align="center" >  


## Joint and link definitions

In URDF the kinematic chain is defined with links and joints between them. To create the kinematic tree in a CAD model that can be later converted to the URDF kinematic chain, we need to add additional "definition" elements to our initial robot CAD shape elements. The basis for this is the definition of the joints tree structure in the robot CAD model. Each separate joint in the later URDF kinematic is represented with a separate CAD element, and the later URDF kinematic links between these joints are created from the initial relations between the CAD joints elements.

All joints "description" CAD elements need to be in the subassembly with the name "urdf*" or "URDF*". This subassembly needs to be created on the top level of the CAD tree, like in the image:

<img src="./figures/tree_clean.PNG" 
     height="300"   align="center" >  <img src="./figures/tree_urdf.PNG" 
     height="300"   align="center" >  

Each created joint CAD element needs to be named "joint_PARENT_to_CHILD_*". Where "joint_" and "\_to_" are joint tags and "PARENT" and "CHILD" are urdf links names of your choice, that the defined joint is connecting. As per convention, "\*"  after the last underscore can be substituted with anything. Special joint definitions "joint_base_*" also need to be added, that mark the origin of the whole URDF coordinate system and root of the kinematic tree.

Joint definitions define the URDF kinematics chains by defining a child from the previous joint as a parent in the next one. The chain of definitions should start with the link "base" from "joint_base_*" and be unbroken to the end nodes. The kinematic tree can be branched to different end nodes.

### Joint definition CAD element

The joint definition CAD element needs to be created as the subassembly, as the name of the part inside the joint subassembly defines the joint type. Currently, the following three joint types are supported: fixed, revolute, and prismatic with corresponding parts names "fixed*", "revolute*" and "prismatic*".

The coordinate system of the subpart represents the joint coordinate system in URDF definitions. In the case of the revolute and prismatic axis, the x-axis is the rotation axis or the direction of translational movement.

The shape in the joint subassembly is saved to the STEP file, but it is later ignored in the URDF creation, so any user may choose his own desired shapes inside joints definitions. Because the Fusion 360 doesn't allow to save the part with no shape to the STEP file, we added the ball shape to the part representing the joint type. 

<img src="./figures/joint_cad_definition.PNG" 
     height="300"   align="center" >  


We created one CAD joint definition that we mated as an independent copy for all our joint definitions. For each copy, we changed the subassembly name to the required link names that it was connecting, and we changed the internal part name to the joint type that it was representing. 


### Link shapes definitions

Kinematic links for URDF are created automatically from the joints elements relations. With the link "definition" element, we only need to connect different parts of our initial robot CAD shape to corresponding links.

link_LINKNAME_*

Not all link names from URDF assembly definition need to have shape definitions

The shapes than are not hierarchically in any link, they are automatically added to the URDF base link

[//]: # "STL also exported automatic"

TODO: How to export colors.

<img src="./figures/tree_shapes.PNG" 
     height="300"   align="center" >  
