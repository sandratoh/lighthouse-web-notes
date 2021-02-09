# Asynchronous Programming

## What is Asynchronous Programming?

*Definition*: when a unit of work is run separately from the main thread of the program and notifies the program of its completion

*How does it differ from **synchronous programming**?*
Program waits for result of one unit of work before moving onto the next unit. While the first unit runs, the program would sit *idled* or *blocked* (more time-consuming).

## Asynchronous Callbacks

> JavaScript leverages callbacks in order to deal with time consuming tasks.


Dealing with codes in async codes is called **Async Flow Control**: controlling flow of at which the codes run, and set expectations for when things are done