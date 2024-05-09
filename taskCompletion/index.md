# Task Completion

The assignment will be completed using _SOLID_ principles approach.

> Before getting acquainted with Task Completion documentation it is recommend to read why this approach was chosen. You can find approach documentation [here](../approach/index.md).

The main goal of choosing _SOLID_ principles approach is:

- If we need to make a change to `SignupForm`, then such a change should be made in a single place and preferably in such a way that will not change the code that already works. Instead we should be able to add new code that will change the component's behavior.
- It should be possible to create a new version of the component reusing already existing code.
- The risk that new changes will break something should be minimized.
