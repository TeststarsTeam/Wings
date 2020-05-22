C unit test  
=============================================

Naming rules (using Google C++ Style Guide)
-----------------------

1. The generated file directory is shown in Figure 5 below:

.. image:: /image/figure5.png

The unit test code is stored in the drivercode folder.
2. driver.cc and driver.h mainly store some public functions and header files in the program.
3. The same structure or union may be used as the parameters of multiple functions. In order to avoid code duplication, wings are encapsulated into different drive functions or parameter capture functions for all types of structures and unions.

Examples are as follows:

For the structure information in figure 2, 5 different driver function information will be generated, as shown in figure 6 below:

.. image:: /image/figure6.png

The naming rules for structure implementation functions are: DriverStruct+ struct name + type, where Point represents a primary pointer or a one-dimensional array, and PointPoint represents a secondary pointer or a two-dimensional array.For each function, the corresponding driver function is generated.

The naming rules for source files are: driver_ + source file name + .cc

For example: driver_nginx.cc

Driver function naming rules: Driver_ + function name

For example: Driver_ngx_show_version_info (void);

Note: For static test function, it is necessary to remove the static functions
Add the declaration of the source function before the driver function.

For example:extern void ngx_show_version_info(void); 
Driver_ngx_show_version_info(void);

5. output of return value
The naming rule for the printout function of the return value: Driver + Return + Print_ + function name.
For example: DriverReturnPrint_ngx_show_version_info ();

6.The main function in the user source code needs to be commented out manually. Wings will regenerate a main function file in the driver code for testing. Wings will generate the main function file that drives main as : gtest_auto_main.cc
Note: Users choose to use it according to their needs.


Generate code
-----------------------

Function prototype: int coordinate_destory ( location_s * loc, size_t length, char * ch )
The type of the return value is int , the type of the first parameter is location * , the type of the second parameter is size_t , and the type of the third parameter is char *
Assign values to the above three parameters.

The complete drive code  for the coordinate_destory function is described in detail in Figure 7 below . 

.. image:: /image/figure7-1.png

.. image:: /image/figure7-2.png

