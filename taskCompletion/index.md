# Task Completion

The assignment will be completed using _SOLID_ principles approach.

> Before getting acquainted with Task Completion documentation it is recommend to read why this approach was chosen. You can find approach documentation [here](../approach/index.md).

The main goal of choosing _SOLID_ principles approach is:

- If we need to make a change to `SignupForm`, then such a change should be made in a single place and preferably in such a way that will not change the code that already works. Instead we should be able to add new code that will change the component's behavior.
- It should be possible to create a new version of the component reusing already existing code.
- The risk that new changes will break something should be minimized.

## Components Documentation

Components list with naming (real names):

- [SignupForm](#signupform)
- [TextInput](#textinput)\*
- [SubmitButton](#submitbutton)\*

- [useSignupFormStore](#usesignupformstore-tinitialstate-formstatet--signupformstore)
- [validateSignupForm](#validatesignupform-values-signupformvalues--partialsignupformvalues)
- [submitCredentials](#submitcredentials-username-string-password-string--promiseunknown)

\* - a reusable component

### SignupForm

This component is responsible for constructing a specialized form component by reusing various parts of already existing code. In order to render UI it uses `TextInput` and `SubmitButton` (both are reusable components). Also this component is responsible for providing general layout and calling functions:

- `useSignupFormStore` - a custom hook used to create form store (form state + state handlers)
- `validateSignupForm` - to get `errors` object
- `submitCredentials` - to submit data to API endpoint

If we want to change general layout somehow or to call another validation function instead of `validateSignupForm`, we should change this component.

### TextInput

An _reusable_ _dumb_ component, responsible to implement _SRP_ principle: to serve as a single place for holding render logic of text input field. In case we want to change somehow how text input field is rendered - we should change `TextInput` component.

### SubmitButton

A _reusable_ _dumb_ component, responsible to implement _SRP_ principle: to serve as a single place for holding submit button render logic. In case we want to change somehow how submit button is rendered - we should change `SubmitButton` component.

### useSignupFormStore: `<T>(initialState: FormState<T>) => SignupFormStore`

A custom generic react hook responsible to implement _SRP_ principle: to serve as a single place for creating and holding form store logic.

Form state is created based on `SignupFormValues` type.

If we want to change somehow how store is updated, we should do it here.

### validateSignupForm: `(values: SignupFormValues) => Partial<SignupFormValues>`

A function responsible to implement _SRP_ principle: to serve as a single place for holding validation logic and creating a form errors object. If we want to change validation logic (e.g. error message or add additional validation), we should do it here.

### submitCredentials: `(username: string, password: string) => Promise<unknown>`

A function responsible to implement _SRP_ principle: to serve as a single place for calling an API endpoint and submitting form data.
