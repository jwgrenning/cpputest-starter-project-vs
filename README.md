cpputest-starter-project-vs
===========================

A cpputest starter project with instructions for visual studio

Create Your First Legacy C/C++ Test Project - Visual Studio

This describes how to integrate CppUTest based testing into your production code base using the Visual Studio environment.  I'll assume you are using Visual Studio 2010 in the instructions, but there are project files for VS2008 and VC6. As a reference, here are the other Visual Studio file extensions:

	•	VC6 file extensions (dsw, dsp)
	•	VS2008 file extensions (sln, vcproj)
	•	VS2010 file extensions (sln, vcxproj)

Install and build CppUTest
Go to cpputest.org, and download the latest cpputest.  
Follow the instructions for building it.
Add an environment variable called CPPUTEST_HOME to your environment variables that points the home directory of CppUTest.

Unzip and build the starter project
Test files and production code files should all be kept in version control.  Assuming your code is already in version control (if not, why not?!), this section describes how to integrate testing into your source repository.

Move starter test files to your production code repository
Test files and production code files should all be kept in version control.  Assuming your code is already in version control (if not, why not?!), this section describes how to integrate testing into your source repository.

Let's presume a directory structure like this:

	ProductRepository
		|-- include
		|-- source

Copy the following files to your ProductRepository

	•	TddC-StarterProject_VS2010.sln (VS2010)
	⁃	TddC-StarterProject_VS2008.sln
	⁃	TddC-StarterProject.dsw
	•	tests
	•	test/*.cpp
	•	tests/AlTests.vcxproj (VS2010)
	•	ProductionCodeLib
	•	ProductionCodeLib/ProductionCodeLib.vcxproj
	•	SomeDirectory/example.c

Add a directory called 'lib' to ProductSourceRepository

You should now have this directory structure (assuming VS2010)

	ProductSourceRepository
		|-- include
		|-- lib
		|-- source
		|-- mocks
		|-- tests
			|-- AllTests.cpp
			|-- MyFirstTest.cpp
			|-- AlTests.vcxproj (VS2010)
		|-- ProductionCodeLib
			|-- ProductionCodeLib.vcxproj (VS2010)
		|-- SomeDirectory
			|-- example.c
		|-- TddC-StarterProject_VS2010.sln


Test your initial setup

Rebuild all with Visual Studio.  You should see these test results in the console window:

	compiling MyFirstTest.cpp
	Linking MyProductTests_tests
	Running MyProductTests_tests
	.
	OK (1 tests, 1 ran, 0 checks, 0 ignored, 0 filtered out, 0 ms)

Cause the test to fail.  Open example.c, change the return result to 0.  You should see:

	compiling MyFirstTest.cpp
	Linking MyProductTests_tests
	Running MyProductTests_tests

	tests/MyFirstTest.cpp:28: error: Failure in TEST(MyCode, test1)
		expected <1 0x1>
		but was  <0 0x0>

	.
	Errors (1 failures, 1 tests, 1 ran, 0 checks, 
					0 ignored, 0 filtered out, 1 ms)

Restore the example()'s return result to 1 and see tests pass again.

Things that can go wrong:
	•	You build fails because it cannot find CppUTest includes
	⁃	Define the environment variable CPPUTEST_HOME to be equal to the location of CppUTest


