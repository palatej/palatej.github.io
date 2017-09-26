---
layout: left-menu
title: Householder reflection
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Householder reflection
order: 100
category: Elementary transformations
---
# {{page.description}}

<hr>

#### Implementations

Householder reflections are implemented in the class `demetra.maths.matrices.HouseholderReflection`

Example

```java
        DataBlock x=DataBlock.make(10);
        Random rnd=new Random();
        x.set(rnd::nextDouble);
        double nx=x.norm2();
        // Creates the Householder reflection
        HouseholderReflection hr = HouseholderReflection.of(x);
        // x is now (|| x || 0 ... 0)
        assertTrue(x.drop(1, 0).allMatch(z->z==0));
        assertEquals(nx, x.get(0), 1e-9);
        // apply the transformation on another vector
        DataBlock y=DataBlock.make(10);
        y.set(rnd::nextDouble);
        hr.transform(y);

```