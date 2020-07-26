# Internship Notes

## Hashing

Hashing is an improvement over Direct Access Table. The idea is to use hash function that converts a given phone number or any other key to a smaller number and uses the small number as index in a table called hash table.

#### Hash Function

A function that converts a given big phone number to a small practical integer value. The mapped integer value is used as an index in hash table. In simple terms, a hash function maps a big number or string to a small integer that can be used as index in hash table.

A good hash function should have following properties:

1. Efficiently Computable
2. Should Uniformly Distribute Keys

## Concurrency

#### Race Condition

At least 2 processes working on a shared piece of data, and eventual output is dependant on the order in which these process are run.
This will lead to data inconsistency, which we cannot afford to have.

This is the problem that we have to solve.

This problem happened because these processes were working on shared data.
If we restricted this access, ie, if we didnt let 2 processes work on same data at the same time then this problem will be solved.

##### Critical Section Problem

If you have 2 processes, p1 and p2, and both these processes have critical sections, cs1 and cs2 (critial section: Part of code which accesses the shared data).
Now problem reduces to: Making these critical sections work sequentially

We can have a flag. As long as flag is 1, that means someone else is using the Critical section, once it's 0, only then it can be used

```c++
1. while(flag == 0) {
2.    flag = 1;
3.    cs;
4.    flag = 0;
5. }
```

If we can have a condition that while loop check and flag = 1 can only either both be executed, or none of them be executed.

ie, make line 1 and 2 Atomic. If a set of instructions are atomic, you cannot divide them further. So, either all of them will execute or none of them will execute.

##### Who can make this atomic? Which entitity is responsible to make this atomic?

Our Program cannot make this atomic, as it is running on the system.
The Entitiy which runs it can make it atomic. The Entitiy which schedules these processes can do this. This entity is OS.

We are reliant on the OS to ensure that line 1 and 2 are atomic.

This is known as a **Mutex Lock**. Program can communicate to OS about what it wants to be atomic, OS then makes it atomic.

**Mutex Lock** is known as Mutual Exclusion Law

We are testing a variable, and then setting the value of it. This is known as testing and setting.

What facility do we want from the OS?
If a program calls a function "Lock", the OS should check for the shared variable, and block if the shared variable is being used, if not, set it, and come out.
