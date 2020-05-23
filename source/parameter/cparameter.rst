C language parameter capture  
=============================================
The wings parameter capture function is mainly to obtain the function parameter value, global variable value and return value information at runtime.


Naming rules for parameter capture code
-----------------------
The parameter capture code for wings is stored in the paramcaputrecode folder. The naming rules are the same as the driver format, and all driver can be replaced with param.


Example of parameter capture code
-----------------------

As shown in below, for the function coordinate_destroy , information about capture parameters, global variables, and return values is automatically generated.

::

	#ifndef _PARAMCAPTURE_WINGS_C_DEMO_COORDINATES_H_
	#define _PARAMCAPTURE_WINGS_C_DEMO_COORDINATES_H_
	#include "ParamCapture.h"
	#include "ParamCapture_structorunion.h"
	void ReturnCapture_coordinate_create(coordinate_s returnType);

	void ParamCapture_coordinate_destroy(location *loc, size_t length, char *ch);
	void GlobalCapture_coordinate_destroy(int count);
	void ReturnCapture_coordinate_destroy(int returnType);

	void ParamCapture_func_point(double param1, int param2);
	void ReturnCapture_func_point(void returnType);
	#endif // WINGS_C_DEMO_COORDINATES

Figure below will show the automatically generated code for capturing parameters.

::

	int coordinate_destroyTimes = -1;
	void ParamCapture_coordinate_destroy(location *loc, size_t length, char *ch)
	{
		coordinate_destroyTimes++;
		const char *jsonFile = "paramcapturevalue/wings_c_dem_coordinates/coordinate_destroy.json";
		cJSON *root = NULL;
		if (coordinate_destroyTimes == 0){     
			root = cJSON_CreateObject();
		}else{
			char *jsonData = ParamCaptureGetJsonData(jsonFile);
			root = cJSON_Parse(jsonData);
		}
		int coordinate_destroy_len = strlen("coordinate_destroy");
		char *coordinate_destroy_sp = (char *)malloc(sizeof(char) * (coordinate_destroy_len + 2));
		sprintf(coordinate_destroy_sp, "coordinate_destroy%d", coordinate_destroyTimes);
		cJSON *item = cJSON_CreateObject();
		cJSON_AddItemToObject(root, coordinate_destroy_sp, item);
		free(coordinate_destroy_sp);
		/*It is the 1 parameter: loc */
		cJSON *location_sitem = cJSON_CreateArray();
		Struct_location_s_P(location_sitem, loc, 1);
		cJSON_AddItemToObject(item, "loc", location_sitem);
		/*It is the 2 parameter: length*/
		cJSON_AddItemToObject(item, "length", cJSON_CreateNumber(length));
		/*It is the 3 parameter: ch */
		cJSON_AddItemToObject(item, "ch", cJSON_CreateString(ch));
		FILE *fp;
		fp = fopen(jsonFile, "w");
		fprintf(fp, "%s\n", cJSON_Print(root));
		fclose(fp);
	}



