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

For the structure information in figure 2, 5 different driver function information will be generated, as shown in below:
::

  struct coordinate_s DriverStructcoordinate_s(cJSON *coordinate_sRoot);
  struct coordinate_s *DriverStructcoordinate_sPoint(cJSON *coordinate_sRootPoint, int row);
  struct coordinate_s **DriverStructcoordinate_sPointPoint(cJSON *coordinate_sRootPointPoint, int row, int column);


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

The complete drive code  for the coordinate_destory function is described in detail in below . 

::

  extern int coordinate_destroy(location *loc, size_t length, char *ch);
  int coordinate_destroy_intTimes = 0;
  int Drive_coordinate_destroy(int times)
  {
      coordinate_destroy_intTimes = times;
      /* Root is the json object of the value file.coordinate_destroy_int_Root is function.coordinate_destroy_int is json object.  */
      const char *jsonFile = "../drivervalue/wings_c_demo_coordinates/coordinate_destroy_int.json";
      char *json_data = get_json_data(jsonFile);
      cJSON *Root = cJSON_Parse(json_data);
      int coordinate_destroy_int_len = strlen("coordinate_destroy_int");
      char *coordinate_destroy_int_sp = (char *)malloc(sizeof(char) * (coordinate_destroy_int_len + 3));
      sprintf(coordinate_destroy_int_sp, "coordinate_destroy_int%d", times);
      cJSON *coordinate_destroy_int_Root = cJSON_GetObjectItem(Root, coordinate_destroy_int_sp);
      free(coordinate_destroy_int_sp);
      /*It is the 1 global variable: count    coordinate_destroy */
      int _count = cJSON_GetObjectItem(coordinate_destroy_int_Root, "count")->valueint;
      count = _count;
      /*It is the 1 parameter: loc    coordinate_destroy*/
      cJSON *loc_Arr_Root = cJSON_GetObjectItem(coordinate_destroy_int_Root, "loc");
      int loc_size = cJSON_GetArraySize(loc_Arr_Root);
      struct location_s *_loc = DriverStructlocation_sPoint(loc_Arr_Root, loc_size);
      /*It is the 2 parameter: length    coordinate_destroy*/
      unsigned int _length = (unsigned int)cJSON_GetObjectItem(coordinate_destroy_int_Root, "length")->valueint;
      /*It is the 3 parameter: ch    coordinate_destroy*/
      char *_ch;
      {
          char *_ch_str = cJSON_GetObjectItem(coordinate_destroy_int_Root, "ch")->valuestring;
          _ch = (char *)malloc(sizeof(char) * (strlen(_ch_str) + 1));
          memcpy(_ch, _ch_str, strlen(_ch_str));
          _ch[strlen(_ch_str)] = '\0';
      }
      //Function Call
      int returnType = coordinate_destroy(_loc, _length, _ch);
      return 0;
  }

::

  struct location_s *DriverStructlocation_sPoint(cJSON *location_sRootPoint, int row)
  {
      struct location_s *_location_s = (struct location_s *)malloc(sizeof(struct location_s) * row);
      for (int i = 0; i < row; i++)
      {
          cJSON *location_s_Root = cJSON_GetArrayItem(location_sRootPoint, i);
  
          int **_mPoi;
          cJSON *mPoi_Root = cJSON_GetObjectItem(location_s_Root, "mPoi");
          int mPoi_row = cJSON_GetArraySize(mPoi_Root);
          _mPoi = (int **)malloc(sizeof(int *) * mPoi_row);
          for (int i = 0; i < mPoi_row; i++)
          {
              cJSON *mPoi_Root_Row = cJSON_GetArrayItem(mPoi_Root, i);
              int mPoi_column = cJSON_GetArraySize(mPoi_Root_Row);
              _mPoi[i] = (int *)malloc(sizeof(int) * mPoi_column);
              for (int j = 0; j < mPoi_column; j++)
              {
                  _mPoi[i][j] = cJSON_GetArrayItem(mPoi_Root_Row, j)->valueint;
              }
          }

          _location_s[i].mPoi = _mPoi;
          cJSON *coor_Arr_Root = cJSON_GetObjectItem(location_s_Root, "coor");

          int coor_size = cJSON_GetArraySize(coor_Arr_Root);
          struct coordinate_s *_coor = DriverStructcoordinate_sPoint(coor_Arr_Root, coor_size);

          _location_s[i].coor = _coor;
          cJSON *pf_Arr_Root = cJSON_GetObjectItem(location_s_Root, "pf");
          cJSON *pf_Root = cJSON_GetArrayItem(pf_Arr_Root, 0);

          /* wingsParam1 */
          unsigned char *_wingsParam1;
          {
              char *_wingsParam1_str = cJSON_GetObjectItem(pf_Root, "wingsParam1")->valuestring;
              _wingsParam1 = (unsigned char *)malloc(sizeof(unsigned char) * (strlen(_wingsParam1_str) + 1));
              memcpy(_wingsParam1, (unsigned char *)_wingsParam1_str, strlen(_wingsParam1_str));
              _wingsParam1[strlen(_wingsParam1_str)] = '\0';
          }

          /* wingsParam2 */
          unsigned char *_wingsParam2;
          {
              char *_wingsParam2_str = cJSON_GetObjectItem(pf_Root, "wingsParam2")->valuestring;
              _wingsParam2 = (unsigned char *)malloc(sizeof(unsigned char) * (strlen(_wingsParam2_str) + 1));
              memcpy(_wingsParam2, (unsigned char *)_wingsParam2_str, strlen(_wingsParam2_str));
              _wingsParam2[strlen(_wingsParam2_str)] = '\0';
          }
          struct _iobuf *_pf = _iobufFunctionPointer(_wingsParam1, _wingsParam2);

          _location_s[i].pf = _pf;
          cJSON *next_Arr_Root = cJSON_GetObjectItem(location_s_Root, "next");

          int next_size = cJSON_GetArraySize(next_Arr_Root);
          struct location_s *_next = DriverStructlocation_sPoint(next_Arr_Root, next_size);

          _location_s[i].next = _next;
      }
      return _location_s;
  }


