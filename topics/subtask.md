# How to Use Subtasks

A complex task can be broken down into multiple simple subtasks, which can reduce complexity, increase reusability, and allow for flexible and efficient scheduling and execution.

### Types of subtabks
**Asynchronous vs Synchronous**: If the parent task waits for the subtask to complete before continuing execution, the subtask is considered a synchronous subtask; otherwise, it is called an asynchronous subtask. Subtasks using [pop-up web pages](/topics/popup) are all synchronous subtasks.
**Independent vs Member**: If the execution result of a subtask is considered part of the parent task, it is called a member subtask; otherwise, it is called an independent subtask. All asynchronous subtasks are independent subtasks.

Subtasks include the following types:
* **Normal subtask**: aka asynchronous and independent subtask; for example, the parent task reads a file containing a list of product IDs, and then adds a subtask for each product ID to scrape product details.
* **Member subtask**: aka synchronous member subtask
* **Synchronous subtask**: aka synchronous and independent subtask

### How to add subtasks
* Add independent subtask(norml or synchronous task): use action_subtask.subtask
* Add member subtask: use action_setvar_subtask.subtask or action_extract.column_subtask.subtask


Refer to the video on [how to use subtasks](https://youtu.be/7jTd8VYRJH8).
