+++
title='Subtypes'
summary='Like ada'
+++

> You can, and should, define your own types for the domain you are
> modelling. But you can use the standard types to start with and then
> replace them later with your own types, this could be called a form of
> gradual typing.

> The standard types would only really be a good starting point for binding
> to other languages, like C.


```ada
type Degrees is range 0 .. 360;
```
> This is a type. Its underlying representation is an Integer.

```ada
type Hues is (Red, Green, Blue, Purple, Yellow);
```
> So is this. Here, we are declaring an Enumeration.

```ada
type Degrees_Wrap is mod 360;
```
> This is a modular type. They behave like Integers that automatically
> wrap around. In this specific case, the range would be 0 .. 359.
> If we added 1 to a variable containing the value 359, we would receive
> back 0. They are very useful for arrays.

```ada
type Real_Angles is digits 3 range 0.0 .. 360.0;
type Fixed_Angles is delta 0.01 digits 5 range 0.0 .. 360.0;
```
> Yes, you can even define your own floating and fixed point types, this
> is a very rare and unique ability. "digits" refers to the minimum
> digit precision that the type should support. "delta" is for fixed
> point types and refers to the smallest change that the type will support.

https://learnxinyminutes.com/ada/