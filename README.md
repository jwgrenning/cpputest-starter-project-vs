cpputest-starter-project-vs
===========================

A cpputest starter project with instructions for Visual Studio

Create Your First Legacy C/C++ Test Project - Visual Studio

This describes how to integrate CppUTest based testing into your production code base using the Visual Studio environment.  I'll assume you are using Visual Studio 2010 in the instructions, but there are other project files. As a reference, here are the other Visual Studio file extensions:

	• VC6 file extensions (dsw, dsp)
	• VS2008 file extensions (sln, vcproj)
	• VS2010 file extensions (sln, vcxproj)
	• VS2012 file extensions (sln, vcxproj)
	• VS2019 file extensions (sln, vcxproj)

### Install and build CppUTest
* Go to cpputest.org, and download the latest cpputest.  
* Follow the instructions for building it.
* Add an environment variable called CPPUTEST_HOME to your environment variables that points the home directory of CppUTest.
* Open the CppUTest visual studio solution. (e.g., CppUTest_VS201x.sln)
* Make sure to upgrade the current Visual Studio tools. (e.g., for Visual Studio 2019: right-click the solution, and then select "Retarget solution")
* Build: "Menu Debug, Start Without Debugging" (assuming VS 2019)
* You should see these test results in the console window:

    ```
    ...................................
    OK (1085 tests, 1037 ran, 2505 checks, 48 ignored, 0 filtered out, 331 ms)
    ```

### Unzip and build the starter project
* open the solution vs-test-build/TddC-StarterProject_VS2010.sln (or the solution best suited to your VS version)
* Make sure to upgrade the current Visual Studio tools. (e.g., for Visual Studio 2019: right-click the solution, and then select "Retarget solution")
* Build: "Menu Debug, Start Without Debugging" (assuming VS 2019)
* You should see these test results in the console window:

    ```
    ..
    OK (2 tests, 2 ran, 1 checks, 0 ignored, 0 filtered out, 0 ms)
    ```

## How to integrate testing into your source repository.
* Move starter test files to your production code repository
* Test files and production code files should all be kept in version control.
* Assuming your code is already in version control (if not, why not?!), this section describes how to integrate testing into your source repository.
* Let's presume a directory structure like this:

    ```
    ProductRepository
        |-- include
        |-- source
    ```
* Add a directory called 'tests' to ProductSourceRepository
* Add a directory called 'example-src' to ProductSourceRepository
* Add a directory called 'vs-test-build' to ProductSourceRepository
* Copy the following files to your ProductRepository

    ```
        • example-include/example.h
        • example-include/io.h
        • example-platform/io.c
        • example-src/example.c
        • tests/*.cpp
        • vs-test-build/AllTests.vcxproj (VS2010)
        • vs-test-build/ProductionCodeLib.vcxproj (VS2010)
        • vs-test-build/TddC-StarterProject.dsw
        • vs-test-build/TddC-StarterProject_VS2010.sln (VS2010)
    ```
* You should now have this directory structure (assuming VS2010)

```
    ProductSourceRepository
        |-- example-include
	    |-- example.h
	    |-- io.h
        |-- example-platform
	    |-- io.c
        |-- example-src
            |-- example.c
        |-- include
        |-- source
        |-- tests
            |-- AllTests.cpp
	    |-- ExampleTest.cpp
            |-- MyFirstTest.cpp
	|-- vs-test-build
            |-- AllTests.vcxproj
	    |-- ProductionCodeLib.vcxproj
            |-- TddC-StarterProject.dsw
            |-- TddC-StarterProject_VS2010.sln
```
* Open the TddC-StarterProject_VS2010.sln
* Right-click on the solution and select "Clean all"
* Build the solution: "Menu Debug, Start Without Debugging"
* You should see these test results in the console window:

    ```
    ..
    OK (2 tests, 2 ran, 1 checks, 0 ignored, 0 filtered out, 2 ms)
    ```
* Cause the test to fail.  Open example.c, change the return result to 0.  You should see:

    ```
    .
    tests\ExampleTest.cpp(21): error: Failure in TEST(Example, test1)
            expected <1 0x1>
            but was  <0 0x0>
    
    .
    Errors (1 failures, 2 tests, 2 ran, 1 checks, 0 ignored, 0 filtered out, 14 ms)
    ```
* Restore the example()'s return result to 1 and see tests pass again.

## Things that can go wrong:
* You build fails because it cannot find CppUTest includes
  * Define the environment variable CPPUTEST_HOME to be equal to the location of CppUTest

* Visual Studio Intellisense won't work properly / Code Navigation does not work
  * The the .vs folder or the .suo file contains cached IntelliSense data
  * Shut down the Visual Studio
  * Delete the .vs folder or the .suo file
  * Restart the Visual Studio
