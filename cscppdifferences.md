# Differences between C# and C++
Below we will talk about the differences you have to get used to when dealing with C++.

## Header and CPP file
In C++ we split our functions into two files.

### .cpp
This would be where we do the bulk of our programming, tt contains our definitions, equivalent to the .CS file in C#

### .h (Header)
This is an extra file, it conains our declarations. There is no equivalent in C# for this file. The C++ complier is more basic compared to C#, it only wants to run through our code once. In the header file, the complier learns about what the signature of our class is going to look like (declarations). Then once the complier gets to the .cpp file, it will already know what to expect.

We use the Header .h file to set up our class with variables and functions/methods.

## Functions with ::


## *variable

## &variable

## -> vs .

## #pragma once

## #include 

## class above our header file class


## :: scope resolution operator
`FMath::Sin(float x);`
The :: allows you to specify the scope of the variable or function. For example, Sin() function from FMath.

https://learn.microsoft.com/en-us/windows/win32/multimedia/the-scope-resolution-operator-in-c
