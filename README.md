# Python-Guidelines
Abstract
Ignoring a condition can cause the program to overlook unexpected states and errors.
Explanation
Just about every serious attack on a software system begins with the violation of a programmer's assumptions. After the attack, the programmer's assumptions seem flimsy and poorly founded, but before an attack many programmers would defend their assumptions well past the end of their lunch break.

Two dubious assumptions that are easy to spot in code are "this method call can never fail" and "it doesn't matter if this call fails". When a programmer ignores a condition, they implicitly state that they are operating under one of these assumptions.

Example 1: The following code excerpt ignores an error condition that might happen during a CICS transaction.
