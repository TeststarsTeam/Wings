C ++ parameter capture 
=============================================


C ++ parameter capture code naming rules
-----------------------
The naming rules for parameter capture of c ++ are the same as that of the driver, just replace the driver with paramcaputre .


C ++ parameter capture code description
-----------------------
For each class, a parameter capture class is generated, and each function in the capture class will generate a function that captures parameters, global variables, and return values.

::

	#pragma once
	#include "paramcapture.h"
	class ParamCaptureRectangle
	{
		public:
		ParamCaptureRectangle();
		 ~ParamCaptureRectangle();
				
		void ParamCapture_GetVolume0();
		void GlobalCapture_GetVolume0();
		void ReturnCapture_GetVolume0(int returnType);
					
		void ParamCapture_PrintVolume1(Rectangle *rect,int parm);
		void GlobalCapture_PrintVolume1();
		void ReturnCapture_PrintVolume1();
	};


How to capture a member variable of a class, a capture function is inserted in the class to obtain the private member variable of the class, as shown in Figure 20 :

::

	class Rectangle
	{
	private:
		Point *m_point;
		int m_z;
		std::string name;
	public:
		Rectangle();
		int GetVolume();
		void PrintVolume(Rectangle *rect, int parm);
	public:
		Rectangle(Point *m_point, int m_z, std::string name, bool wings)
		{
			//LOGI("Rectangle::Rectangle");
			this->m_point = m_point;
			this->m_z = m_z;
			this->name = name;
		}
		Json::Value W_MemberVarCaputre()
		{
			Json::Value Rectangle_Root;
			Rectangle_Root["m_point"]=m_point->W_MemberVarCaputre();
			Rectangle_Root["m_z"]=Json::Value(m_z);
			Rectangle_Root["name"]=Json::Value(name);
			return Rectangle_Root;
		}
	};


