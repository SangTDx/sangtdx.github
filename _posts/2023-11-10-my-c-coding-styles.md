---
layout: post
title: C Coding Comment Template
date: 2023-11-10 00:00:00
categories: [programming]
tags: [programming]
last_modified_at: 2023-11-10
---

### Header file

{% highlight c %}
/*----------------------------------------------------------------------------*/
/**
 * @file my_header.h
 * @brief This header file contains function and variable declarations used
 *        in the project, serving as an interface between different source files.
 *
 * @copyright [Year] [Your Company/Your Name]
 * @author Your Name
 * @date November 25, 2023
 */
/*----------------------------------------------------------------------------*/

#ifndef MY_HEADER_H
#define MY_HEADER_H

/*----------------------------------------------------------------------------*/
/* Include Headers                                                            */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Include headers required for the project functionality.
 */
#include "header1.h"
#include "header2.h"

/*----------------------------------------------------------------------------*/
/* Constants and Macros                                                       */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Define project-specific constants and macros.
 */
#define MAX_SIZE 100

/*----------------------------------------------------------------------------*/
/* Data Types                                                                 */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Define custom data types used in the project.
 */
struct MyStruct {
    int member1;
    char member2;
};

/*----------------------------------------------------------------------------*/
/* Function Declarations                                                      */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Declare functions used in the project.
 */
void my_function1();
int my_function2(int a, int b);

/*----------------------------------------------------------------------------*/
/* Global Variables                                                           */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Declare global variables used in the project.
 */
extern int g_variable;

#endif // MY_HEADER_H

{% endhighlight %}

### Source file

{% highlight c %}
/*----------------------------------------------------------------------------*/
/**
 * @file my_source.c
 * @brief This source file contains the implementation of functions declared
 *        in the corresponding header file (my_header.h).
 *
 * @copyright [Year] [Your Company/Your Name]
 * @author Your Name
 * @date November 25, 2023
 */
/*----------------------------------------------------------------------------*/

/*----------------------------------------------------------------------------*/
/* Include Headers                                                            */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Include the corresponding header file.
 */
#include "my_header.h"

/*----------------------------------------------------------------------------*/
/* Constants and Macros                                                       */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Define project-specific constants and macros.
 */
#define MAX_SIZE 100

/*----------------------------------------------------------------------------*/
/* Data Types                                                                 */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Define custom data types used in the project.
 */
struct MyStruct {
    int member1;
    char member2;
};

/*----------------------------------------------------------------------------*/
/* Function Declarations                                                      */
/*----------------------------------------------------------------------------*/
/** 
 * @brief Declare functions used in the project.
 */
void my_function1();
int my_function2(int a, int b);

/*----------------------------------------------------------------------------*/
/* Static Variables                                                           */
/*----------------------------------------------------------------------------*/
/** 
 * @brief This section defines static variables used internally in this file.
 * 
 * These variables are declared with the 'static' keyword and are accessible 
 * only within the scope of this file.
 */
static int static_variable = 0;         /**< Description of staticVariable1 */
static char static_variable2 = 'A';     /**< Description of staticVariable2 */

/*----------------------------------------------------------------------------*/
/* Function Implementations                                                   */
/*----------------------------------------------------------------------------*/
/**
 * @brief Implementation of my_function2.
 * @param1: (IN) Description of the first parameter.
 * @param2: (OUT) Description of the second parameter.
 * @param3: (IN/OUT) Description of the second parameter.
 *
 * Detailed description of the function and its behavior.
 *
 * @return: Description of the return value or what it signifies.
 *
 * Written by [Your Name]
 */
int my_function2(int a, int b) {
    // Implementation of the addition operation
    return a + b;
}

{% endhighlight %}

### Reference Link

[https://www2.cs.arizona.edu/~mccann/styletemplatesCP.html](https://www2.cs.arizona.edu/~mccann/styletemplatesCP.html)

[https://github.com/MaJerle/c-code-style](https://github.com/MaJerle/c-code-style)

[https://users.ece.cmu.edu/~eno/coding/CCodingStandard.html](https://users.ece.cmu.edu/~eno/coding/CCodingStandard.html)
