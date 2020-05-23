Introduction to GoogleTest code
=============
In order to compare whether the return value meets the expected output, wings combines the test framework of GoogleTest to automatically complete the writing of the return value and the expected output code.

C language GoogleTest code
-----------------------
gtest_auto_main.cc this file is the entry file for calling GoogleTest . The content is shown in below :

::

	#define _CRT_SECURE_NO_WARNINGS
	#include "gtest/gtest.h"
	#include <stdio.h>
	int main(int argc, char *argv[]) {
	  testing::InitGoogleTest(&argc, argv); 
	  RUN_ALL_TESTS();                      
	  // Start();
	  system("pause");
	  return 0;
	}


For each test .c file, a corresponding driver_ filename_gtest.cc file for function is generated, and the expected comparison operation is performed on the return value of the function coordinate_destory.

In below , the return value of the acquisition function is return , and the expected return value filled in by the user is expected .below is the value file of the measured function.

::

	TEST(wings_c_demo_coordinates, coordinate_destroy)
	{
		for (int times = 0; times < COORDINATE_DESTROY_INT_TIMES; times++)
		{
			Drive_coordinate_destroy_int(times);
			int coordinate_destroy_int_len = strlen("coordinate_destroy_int");
			char *coordinate_destroy_int_sp = (char *)malloc(sizeof(char) * (coordinate_destroy_int_len + 2));
			sprintf(coordinate_destroy_int_sp, "coordinate_destroy_int%d", times);
			const char *jsonFile = "drivervalue/wings_c_demo_coordinates/coordinate_destroy_int.json";
			char *wings_c_demo_coordinates_coordinate_destroy_int_json_data = get_json_data(jsonFile);
			cJSON *Root = cJSON_Parse(wings_c_demo_coordinates_coordinate_destroy_int_json_data);
			cJSON *coordinate_destroy_int_Root = cJSON_GetObjectItem(Root, coordinate_destroy_int_sp);
			free(coordinate_destroy_int_sp);
			int _return_actual = cJSON_GetObjectItem(coordinate_destroy_int_Root, "return")->valueint;
			int _return_expected = cJSON_GetObjectItem(coordinate_destroy_int_Root, "expect")->valueint;
			/* return_expected */
			EXPECT_EQ(_return_expected, _return_actual);
		}
	} 


::

	{
	   "coordinate_destroy_int0" : {
		  "ch" : "JTX",
		  "count" : 8201,
		  "expected" : 10,
		  "length" : 2326,
		  "loc" : [
			 {
				"coor" : [
				   {
					  "mArr" : [
						 [ 6773, 2513, 7989 ],
						 [ 7902, 5447, 4144 ]
					  ],
					  "mInt" : 754,
					  "mPoi" : "_9l",
					  "setx" : null,
					  "vo" : [ 2587, 7670, 6140 ]
				   }
				],
				"mPoi" : [
				   [ 3887, 2125, 6097 ],
				   [ 6496, 8560, 9414 ],
				   [ 8391, 2887, 8267 ]
				],
				"pf" : null
			 }
		  ],
		  "return" : 10
	   }
	}


C++ GoogleTest  code
-----------------------
Each driver class corresponds to a gtest calling class to perform the desired comparison, as shown in below:

::

	#define _SILENCE_TR1_NAMESPACE_DEPRECATION_WARNING 1
	#include "driverRectangle.h"
	#include "gtest/gtest.h"
	class GtestRectangle : public testing::Test {
	protected:
	  virtual void SetUp() {
		const char *jsonFilePath = "../drivervalue/RecordDecl.json";
		Json::Value Root;
		Json::Reader _reader;
		ifstream _ifs(jsonFilePath);
		_reader.parse(_ifs, Root);
		driverRectangle = new DriverRectangle(Root, 0);
	  }
	  virtual void TearDown() { delete driverRectangle; }
	  DriverRectangle *driverRectangle;
	};


The comparison of the gtest function is shown in below :

::

	TEST_F(GtestRectangle, DriverRectangleGetVolume0) {
	  const char *jsonFilePath = "drivervalue/Rectangle/GetVolume0.json";
	  Json::Value Root;
	  Json::Reader _reader;
	  ifstream _ifs(jsonFilePath);
	  _reader.parse(_ifs, Root);
	  for (int i = 0; i < RECTANGLE_GETVOLUME0_TIMES; i++) {
		driverRectangle->DriverRectangleGetVolume0(i);
		Json::Value GetVolume0_Root = Root["GetVolume0" + to_string(i)];
		/* return */
		int _return_actual = GetVolume0_Root["return"].asInt();
		/* expectreturn */
		int _expectreturn_expected = GetVolume0_Root["expect"].asInt();
		/*  */
		EXPECT_EQ(_return_actual, _expectreturn_expected);
	  }
	}

