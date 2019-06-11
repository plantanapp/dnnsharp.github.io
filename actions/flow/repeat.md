# Repeat (For loop / While loop)

> Added in modules released after June 11<sup>th</sup> 2019 ([Action Form 5.0.585+](https://www.dnnsharp.com/download?p=AFORM&v=05.00.585))

The **Repeat** action will help you execute a set of actions in a loop. 
It can act as:
* either a **_For loop_** - repeat for a given number of times
* or a **_While loop_** - repeat while condition is met _(until condition evaluates to false)_
* or a **_For with break loop_** - repeat for a given number of times as long as the codition evaluates to true

depending on the settings provided.

> If the _While Condition_ evalues to false the loop will stop even if it did not finish executing the number of specified steps (_Repetitions_). The same applies when a final action is executed(like _Display toast and stop execution_ or _Display message_)

Providing a base token name is mandatory for the loop to work and you will know the current step of the execution (_repetition_ numer) which is stored in the _[BaseTokenName:CurrentLoopNumber]_ token.

![Repeat action FOR WHILE loop](https://static.dnnsharp.com/documentation/repeat_action_for_while_loop.png)