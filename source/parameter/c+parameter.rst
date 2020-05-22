C ++ parameter capture 
=============================================


C ++ parameter capture code naming rules
-----------------------
The naming rules for parameter capture of c ++ are the same as that of the driver, just replace the driver with paramcaputre .


C ++ parameter capture code description
-----------------------
For each class, a parameter capture class is generated, and each function in the capture class will generate a function that captures parameters, global variables, and return values.

.. image:: /image/figure19.png

How to capture a member variable of a class, a capture function is inserted in the class to obtain the private member variable of the class, as shown in Figure 20 :

.. image:: /image/figure20.png