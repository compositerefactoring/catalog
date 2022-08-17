---
layout: post
title:  Duplicated Parameter Code
category: jekyll
---

# Code Smell

## Description

A method with many lines because one or more parameters require the application of many lines of code, and these lines of code are duplicated in relation to other methods. 

## Abstract Example

The methods `ma()` and `mb()` have a duplicated code because the parameter `bo` is used equally many times and in both methods. This repetitive code related to the parameter `bo` is an example of a Duplicated Parameter Code.

![Abstract Example]({{site.baseurl}}/assets/catalog/duplicated-parameter-code/smell-2-abstract.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Problematic

This code smell degrades the reusability, coupling, size, and cohesion of the method because the method has repetitive code of other methods, and thus it loses the unique responsibility of the method. This decreases the code cohesion, and increases the code size of the method. 

---

# Refactoring

## Name and Description

**Decompose Duplicated Parameter Code**: is the removal of duplicated code, decreasing the method size and increasing code cohesion. This composite refactoring is recommended to remove Duplicated Parameter Code.

## Motivation

The best practices of Oriented Object programming recommend that each method may have a unique feature, and high reusability. For that, it is suggested that each method implements one feature, and it was not long and not duplicated.   

## Mechanics (1)

The developer extracts the duplicated code to another method, applying **Extract Method(s)**. 

### Abstract Example

This is example in which the developer decomposes the Duplicated Parameter Code presented above. The developer extracts the duplicated code to the method `mbo()`, returning `null` case the condition is not satisfied. The method `mbo()` is then called by the methods `ma()` and `mb()`. 

![Mechanics (1) - Abstract Example]({{site.baseurl}}/assets/catalog/duplicated-parameter-code/refactoring-smell2-mechanism1-abstract.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Mechanics (2)

The developer identifies what parameter(s) are requiring many duplicated lines of code. It is necessary to identify if the type of this parameter can be changed to a type that requires few lines of code, or else the method can be divided in other methods. If the parameter(s) can be changed to another type that requires few lines of code, the developer may apply a **Change Parameter Type** on this parameter and **Extract Method** on the duplicated code, separating the repetitive code to a unique method, updating the calls of the source method to the extracted method. If the parameter type cannot be changed, then the developer may apply **Extract Methods**, separating the duplicated code into a unique method. 

### Abstract Example

This is an example in which the developer decomposes the Duplicated Parameter Code presented above. Firstly, the developer applies two Extract Methods from the method `ma()` and `mb()`. The repetitive code was separated to a new method, the mbo()# method. Secondly, the developer updates the parameter type in the methods `ma()` and `mb()` to a type that is not used several and repetitive times in these methods. This parameter is `ao` from the `A` type, thus, the developer changes the parameter type `B` to `A`. 

![Mechanics (2) - Abstract Example - Part 1]({{site.baseurl}}/assets/catalog/duplicated-parameter-code/refactoring-smell2-mechanism2-abstract-part1.png){:style="display:block; margin-left:auto; margin-right:auto"}

![Mechanics (2) - Abstract Example - Part 2]({{site.baseurl}}/assets/catalog/duplicated-parameter-code/refactoring-smell2-mechanism2-abstract-part2.png){:style="display:block; margin-left:auto; margin-right:auto"}

---

# Additional Information

## Concrete Example - Smell

The methods `viewUser()` and `viewClient()` have duplicated code because both methods use the parameter path in the same way. This parameter is used to read the content. Thus, the methods `viewUser()` and `viewClient()` have many lines of repetitive code to read and view content.   

![Concrete Example]({{site.baseurl}}/assets/catalog/duplicated-parameter-code/smell-2-concrete.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Concrete Example - Refactoring (Decompose Duplicated Parameter Code)

This is an example in which the developer decomposes the Duplicated Parameter Code presented above. Firstly, the developer extracts the repetitive code in which the parameter `path` is used. The duplicated code is separated into a new method, the method `getContent()`. This method has the unique responsibility of reading the content. Secondly, the developer updates the parameter type in the methods `viewUser()` and `viewClient()` to the type that is not used many repetitive times in these methods. This parameter has the type `Content`. The developer changes the parameter type `TFile` to `Content`, because the `content` parameter is not used several times in these methods.

![Refactoring - Concrete Example - Part 1]({{site.baseurl}}/assets/catalog/duplicated-parameter-code/refactoring-smell2-mechanism2-concrete-part1.png){:style="display:block; margin-left:auto; margin-right:auto"}

![Refactoring - Concrete Example - Part 2]({{site.baseurl}}/assets/catalog/duplicated-parameter-code/refactoring-smell2-mechanism2-concrete-part2.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Side Effects of Composite

* If the parameter is from an external class, and this parameter calls methods of an external class many times, then these methods can be an envious code. In that case, extractions only can propagate envious code to other methods. The developer can move this envious code if it is necessary.   
* In some cases, if the developer applies only Extract Methods, some duplicated code can continue. 
* If the developer adds many parameters in the extracted methods, then Long Parameter Lists can be introduced in the source code. In that case, the developer can create a method with a short list of parameters to avoid the introduction of Long Parameter Lists. 
* If the extracted methods are long, then Long Methods will be introduced in the source code. Then, the developer may apply more Extract Methods to these long methods.