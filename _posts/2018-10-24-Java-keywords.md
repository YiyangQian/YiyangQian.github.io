---
title: "final, static, this, super"
layout: post
date: 2018-10-25
# image: /assets/images/adsk.JPG
headerImage: false
tag:
- markdown
- components
- extra
category: blog
author: YY
description: Markdown summary with different options
---

## final
* final applies on variable, method and class
    * if the variable is primitive type, cannot change the value.
    * if the variable is a pointer, cannot point it to another object, but internal state of the object can be modified. 
    * when final applies on a class, this class cannot be inherited. All method in a final class will be final method.
    * A final method cannot be overriden by subclasses.  

## static
* static applies to block, variable, method and nested class
* When a member is declared as static, it can be accessed without an instance. 
* static block 
    * Code inside static block is for initialization of a class(before constructor), and it is only executed one. 
* static method
    * static method is part of the class itself, not belonging to any instance of the class.
    * cannot call non static method in the same class directly. 
    * can only access static data
    * cannot refer to this or super
    * called by Class.method()
* static variable
    * shared by all instances of this class
    * part of the class not part of any instance
    * called by Class.vari
* why we use pulic static void main()
    * we need a start handler for our project, cause it is not possible to instanciate all classes.

## this
* this refers to the current instance
    * this.variable
    * this.method()
* this is optional
    * this makes code readable

## super
* super refers to variable and method in parent class
    * super.variable
    * super.method()
