Unit testing automatic generation technology
=============
Features of wings automatic generation technology
-----------------------
* Wings is an intelligent fully automatic test case driven generation system, and can automatically generate test drivers and parameter capture programs.
* Wings supports the C/C ++ language and can handle any type (built-in type and complex types) of parameters, global variables, and return values.
* Supports visual  data tables for assignment, regardless of the driver itself. Data tables can express data relationships at any depth and level, and users only need to edit the table data.Ability to distinguish between system types and custom types. 
* Support special template assignment for complex system types, such as std::vector, rather than expanding all complex system variables.


The overall framework of wings
----------------------
First of all, wings uses static analysis technology to extract the backbone information of the program under test. The main steps are as follows:

* Get compilation database file for different platforms.
* According to the compiled database file, the static analysis of the source code, the extracted information is stored in the PSD structure.
* Read the PSD structure to generate the driver code, GoogleTest code, and the value file. The generated code compiles with the source code. Finally, the test results are output.
* Read the PSD structure to generate the parameter capture code . The generated code is compiled with the source code to get the parameter values of the program at run time.
.. image:: /image/figure1.jpg
