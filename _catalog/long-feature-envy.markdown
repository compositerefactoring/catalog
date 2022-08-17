---
layout: post
title:  Long Feature Envy
category: jekyll
---

# Code Smell

## Description

**Long Feature Envy** is the method that is long (many lines of code) and has envious code (one or more features) scattered on the method. This is the conjunction of two code smell types, Long Method and Feature Envy.

## Abstract Example

In this case, the method `ma()` from class A calls several methods from class B, thus the method `ma()` is a Long Feature Envy.

![Abstract Example]({{site.baseurl}}/assets/catalog/long-feature-envy/smell1-abstract.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Problematic

This code smell degrades the cohesion, coupling, and readability of the method, because the method implements more than one feature, increasing the code size, code coupling, and decreasing the code cohesion and readability. This smell can be an indicator of an architectural problem because one or more features are grouped in a single method, and a long method is generally um method very complex and highly coupled.

---

# Refactoring

## Name and Description

**Remove Long Feature Envy** is the separation of features in different methods. This composite refactoring is recommended to remove **Long Feature Envy** because it decreases the method size and increases code cohesion. 

## Motivation

The best practices of Oriented Object programming recommend that each method may have high cohesion, high readability, and low coupling. For that, it is suggested that each method implements one feature, and it was not long.   

## Mechanics (1)

The developer may identify Long Feature Envy and apply **Extract Methods** aiming to separate methods by concerns. After, the developer moves these methods to appropriate classes (classes that implement the desired concern). If the source method continues long, she/he may simplify some parts of the method, using some refactorings such as **Merge Variable, Merge Parameters, or Parameterize Variable**. Also, the developer may change the return type (**Change Return Type** refactoring) when the responsibility of the method was changed. 

### Abstract Example

This is an example in which the developer applies one Extract Method and one Move Method to remove a Long Feature Envy presented above. However, there is one call of the method `b3()` that is not refactored, because the call of this method depends on the change applied in variable `a`.

#### Refactoring 1: Extract Method

![Refactoring 1: Extract Method]({{site.baseurl}}/assets/catalog/long-feature-envy/smell1-abstract-mechanism1-refactoring1.png){:style="display:block; margin-left:auto; margin-right:auto"}

#### Refactoring 2: Move Method

![Refactoring 1: Extract Method]({{site.baseurl}}/assets/catalog/long-feature-envy/smell1-abstract-mechanism1-refactoring2.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Mechanics (2)

Another mechanism is the application of the extraction and motion at the same time to another class.

### Abstract Example

This is an example in which the developer applies one Extract and Move Method at the same time to remove a Long Feature Envy presented above, creating the method `mb()` in the class B.  

![Refactoring 2: Example]({{site.baseurl}}/assets/catalog/long-feature-envy/smell1-abstract-mechanism2.png){:style="display:block; margin-left:auto; margin-right:auto"}

---

# Additional Information

## Concrete Example - Smell

The class `LogViewer` is responsible for viewing logs. This class has the method `view()`. The method aims to view a log description. The method `view()` is a long feature envy, because its call several methods from the `Message` class.

![Concrete Example]({{site.baseurl}}/assets/catalog/long-feature-envy/smell1-concrete.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Concrete Example - Refactoring (Remove Long Feature Envy)

This example is related to the previous concrete example of code smell. The developer applies one Extract Method and one Move Method to remove the Long Feature Envy presented above. The developer separates responsibilities to update text from the class Message. Some calls of the class Message are necessary, such as the methods `isValid()` and `getText()`, and they cannot be refactored, but the Long Feature Envy is removed. 

### Mechanics (1)

#### Refactoring 1: Extract Method

![Refactoring 1: Extract Method]({{site.baseurl}}/assets/catalog/long-feature-envy/smell1-concrete-mechanism1-refactoring1.png){:style="display:block; margin-left:auto; margin-right:auto"}

#### Refactoring 2: Move Method

![Refactoring 2: Move Method]({{site.baseurl}}/assets/catalog/long-feature-envy/smell1-concrete-mechanism1-refactoring2.png){:style="display:block; margin-left:auto; margin-right:auto"}

### Mechanics (2)

![Concrete Example: Extract and Move Method]({{site.baseurl}}/assets/catalog/long-feature-envy/smell1-concrete-mechanism2.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Side Effects of Composite

* If the developer moves the extracted methods to inappropriate classes, these methods continue envious. Thus, Feature Envies will be introduced in the source code. 
* If the developer adds many parameters in the extracted methods, then Long Parameter Lists can be introduced in the source code. 
* If the extracted methods are long, then Long Methods will be introduced in the source code. Then, the developer may apply more Extract Methods to these long methods.