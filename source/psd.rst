Parameter Structure Description(PSD)
=============
PSD refers to the description of the source code, including class name, class member variable information, class function information, and various types of information.Type information refers to the data types of function parameters, global variables, and return values. Complex data types are expanded layer by layer to built-in types (char, int, string, and so on).The PSD structure is stored in an XML file, and different XML files store different description information.

RecordDecl.xml: store the analysis and development results of structures ,unions and classes in the entire project.

EnumDecl:store the enumerate information in the entire project.

filename.xml : store function information for each file.

A brief description of some attributes is as follows:

Type attribute

+-------------------------------------------------+------------------------+
|ZOA_CHAR_S/ZOA_UCHAR/ZOA_INT/ZOA_UINT/ZOA_LONG   |                        |
|ZOA_ULONG/ZOA_FLOAT/ZOA_UFLOAT/ZOA_SHOTR         |built-in type           |
|ZOA_USHORT/ZOA_DOUBLE/ZOA_UDOUBLE                |                        |      
+-------------------------------------------------+------------------------+
| StructureOrClassType                            |Structures type         | 
+------------------------+------------------------+------------------------+
| ZOA_FUNC                                        |function pointer type   | 
+------------------------+------------------------+------------------------+
| ZOA_UNION                                       |union type              | 
+------------------------+------------------------+------------------------+
| ZOA_ENUM                                        |enumeration type        | 
+------------------------+------------------------+------------------------+
| ClassType                                       |class type              | 
+------------------------+------------------------+------------------------+


Basetype attribute

+------------------------+------------------------+
| BuiltinType            |built-in type           |               
+------------------------+------------------------+
| ArrayType              |array type              | 
+------------------------+------------------------+
| PointerType            |pointer type            | 
+------------------------+------------------------+
| StructureOrClassType   |Structures type         | 
+------------------------+------------------------+
| UnionType              |union type              | 
+------------------------+------------------------+
| EnumType               |enumeration type        | 
+------------------------+------------------------+
| FunctionPointType      |function pointer type   | 
+------------------------+------------------------+


Other attributes

+---------------------------------+-------------------------------------------------------------------+
| Name                            |Represents the names of structures, classes, and unions            |               
+=================================+===================================================================+
| NodeType                        |linked lists                                                       | 
+---------------------------------+-------------------------------------------------------------------+
| parmType                        |function parameter                                                 | 
+---------------------------------+-------------------------------------------------------------------+
| parNum                          |The number of function                                             | 
+---------------------------------+-------------------------------------------------------------------+
| SystemVar                       |type in system include                                             | 
+---------------------------------+-------------------------------------------------------------------+
| value                           |The value of the enumeration type                                  | 
+---------------------------------+-------------------------------------------------------------------+
| bitfield                        |Bytes occupied by bitfield                                         | 
+---------------------------------+-------------------------------------------------------------------+
| returnType                      |return type                                                        | 
+---------------------------------+-------------------------------------------------------------------+
| Field                           |member of class                                                    | 
+---------------------------------+-------------------------------------------------------------------+
| Method                          |class constructor                                                  | 
+---------------------------------+-------------------------------------------------------------------+
| paramName                       |class constructor parameter name                                   | 
+---------------------------------+-------------------------------------------------------------------+
| paramType                       |class constructor parameter types                                  | 
+---------------------------------+-------------------------------------------------------------------+
| TemplateArgumentType            |Template parameter type                                            | 
+---------------------------------+-------------------------------------------------------------------+
| TemplateArgumentValue           |The parameters in the structure are concrete values                | 
+---------------------------------+-------------------------------------------------------------------+
| FunctionModifiers               |function access                                                    | 
+---------------------------------+-------------------------------------------------------------------+
| FunctionAttribute               |Function is extern or static function                              | 
+---------------------------------+-------------------------------------------------------------------+
| FuncClassName                   |The class to which the function belongs                            | 
+---------------------------------+-------------------------------------------------------------------+
| OperatorFundecl                 |Overload operator functions                                        | 
+---------------------------------+-------------------------------------------------------------------+
| Operator                        |Overload operator types                                            | 
+---------------------------------+-------------------------------------------------------------------+


C language PSD structure description
-----------------------
For complex types, such as the structure type location_s , in addition to the basic data type, the member variable also contains the structure type. In the code shown in the following figure 2, the location_s contains the coordinate_s structure, and FILE and other types of information To distinguish between different types.

.. image:: /image/figure2.png
The PSD storage structure of FIG . 2 above is shown in FIG. 3 , where the description information of the structure mainly includes member variable names, types of member variables, and information such as judging whether the member variable is a system variable or a linked list. For different information, different information processing is done during driver generation or parameter capture.

.. image:: /image/figure3.png


C ++ PSD structure description
-----------------------
C ++ mainly indicates that the type is a class, so the test is that c ++ takes a class as a unit for testing. The class mainly includes the member variable name and type information of the class, and the access permission information of the member variable. The member functions of the class are divided into constructors, inline functions, virtual functions, etc., parameter information and type information of member functions.

.. image:: /image/figure4.png