---
tags:
  - software_design
link: https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial/
---
The [UML](https://en.wikipedia.org/wiki/Unified_Modeling_Language) Class diagram is a graphical notation used to construct and visualize object oriented systems. A class diagram in the Unified Modeling Language (UML) is a type of static structure diagram that describes the structure of a system by showing the system's:

- classes,
- their attributes,
- operations (or methods),
- and the relationships among objects.

## UML Class Notation

A class represent a concept which encapsulates state (**attributes**) and behavior (**operations**). Each attribute has a type. Each **operation** has a **signature**. 
_The class name is the **only mandatory information**_.

![[Pasted image 20240826092030.png]]

**Class Name:**
- The name of the class appears in the first partition.

**Class Attributes:**
- Attributes are shown in the second partition.
- The attribute type is shown after the colon.
- Attributes map onto member variables (data members) in code.

**Class Operations (Methods):**
- Operations are shown in the third partition. They are services the class provides.
- The return type of a method is shown after the colon at the end of the method signature.
- The return type of method parameters are shown after the colon following the parameter name. Operations map onto class methods in code

![[Pasted image 20240826092146.png]]

### Class Visibility
The +, - and # symbols before an attribute and operation name in a class denote the visibility of the attribute and operation.

![[Pasted image 20240826092214.png]]

- + denotes public attributes or operations
- - denotes private attributes or operations
- \\# denotes protected attributes or operations

### Parameter Directionality
Each parameter in an operation (method) may be denoted as in, **out** or **inout** which specifies its direction with respect to the caller. This directionality is shown before the parameter name.\

![[Pasted image 20240826092305.png]]

---
## Relationships between classes
UML is not just about pretty pictures. If used correctly, UML precisely conveys how code should be implemented from diagrams. If precisely interpreted, the implemented code will correctly reflect the intent of the designer. Can you describe what each of the relationships mean relative to your target programming language shown in the Figure below?
If you can't yet recognize them, no problem this section is meant to help you to understand UML class relationships. A class may be involved in one or more relationships with other classes. A relationship can be one of the following types:

![[Pasted image 20240826092409.png]]

### Inheritance (or Generalization):
A generalization is a taxonomic relationship between a more general classifier and a more specific classifier. Each instance of the specific classifier is also an indirect instance of the general classifier. Thus, the specific classifier inherits the features of the more general classifier.

![[Pasted image 20240826092459.png]]

## Class Diagram Example: Order System

![[Pasted image 20240826092528.png]]

![[Pasted image 20240826092541.png]]