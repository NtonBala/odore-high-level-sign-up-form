# Approach

> Test task description can be found [here](../README.md).

## The assignment can be implemented in several ways:

**Common Approach for Not Complex Projects**

If project is not complex (e.g. simple startup case), the assignment can be done with simple `form library + components library` bundle. In this case pros would be:

- high development speed
- low barrier of entry for dev team (low requirements for dev team)

The main cons would be: If project grow complex it's very likely that by that time code will become unmaintainable. A simple reusable component, like `SignupForm` at some point will be overcrowded with various conditions, its code parts will be excessively connected with each other, it will be difficult to understand what exactly its code does. Finally, it will be very difficult to provide changes to such a component as the result of those changes will be unpredictable. In the end, such a simple component will need entire refactoring at some point, which in turn may demand to develop a complex refactoring strategy in order to resolve project components reusability issues.

**Atomic Design Approach**

[This](https://atomicdesign.bradfrost.com/table-of-contents) is probably the most suitable approach for products of high complexity as it allows to develop a full-fledged _designing system_. The main disadvantages will be that team needs capacity to develop the project _designing system_ and a _modular design specialist_. So at first, the development speed will be low (also it may be that project barrier of entry will be high). But in the end, _designing system_ will speed up the development by allowing team to concentrate on complex business logic, architectural patterns and designing high-level components.

**SOLID Principles**

In order to design high-level UI components _SOLID_ principles approach is may be the one of the best, as it allows to avoid most common reusable components issues, such as:

- code contains more and more conditions
- different parts become more and more connected with each other
- it becomes difficult to understand what exactly the code does
- over time it becomes more and more difficult to provide code changes as result of such changes becomes unpredictable

At the same time it is relatively simple to:

- avoid breaking code that already works
- make components reusable in a way when they could be substituted one for the other
- keep interfaces "narrow"
- keep it clear how code changes should be made
- avoid using things that are not needed
- work with abstractions

Besides that _SOLID_ principles may be combined with _atomic design_ language and make code more opened for future change of helper libraries bundles (like [react-hook-form](https://www.react-hook-form.com/) + [MUI](https://mui.com/) e.g.).

## Assignment Completion

For the assignment completion _SOLID_ principles approach will be used as it's not so complex as creating a _designing system_ and at the same time it allows to avoid common startup pitfalls. Documentation for task completion can be found [here](../taskCompletion/index.md).
