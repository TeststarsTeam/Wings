Data table
=============================================
Wings test case data is randomly generated and supports int, char, double, float, bool, char * types. The data table supports editing any value.

1. The wings data table expands layer by layer to basic types for parameters.
2. Pointer types for basic types, such as int * p; wings are processed as one-dimensional array types of indefinite length, int ** p; are processed as two-dimensional array types of indefinite length, the default length is 3 , and the data table interface can be Click to add and delete data.
3. Arrays of indefinite length are used as function parameters, such as int p []; the default length of wings is 1 , and users can add and modify them arbitrarily on the data table interface according to needs.

.. image:: /image/figure28.png
