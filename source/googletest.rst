Introduction to GoogleTest code
=============
In order to compare whether the return value meets the expected output, wings combines the test framework of GoogleTest to automatically complete the writing of the return value and the expected output code.

C language GoogleTest code
-----------------------
gtest_auto_main.cc this file is the entry file for calling GoogleTest . The content is shown in Figure 12 :

.. image:: /image/figure12.png

For each test .c file, a corresponding driver_ filename_gtest.cc file for function is generated, and the expected comparison operation is performed on the return value of the function coordinate_destory.

In Figure 13 , the return value of the acquisition function is return , and the expected return value filled in by the user is expected .Figure 14 is the value file of the measured function.

.. image:: /image/figure13.png

.. image:: /image/figure14.png


C++ GoogleTest  code
-----------------------
Each driver class corresponds to a gtest calling class to perform the desired comparison, as shown in Figure 15

.. image:: /image/figure15.png

The comparison of the gtest function is shown in Figure 16 :

.. image:: /image/figure16.png
