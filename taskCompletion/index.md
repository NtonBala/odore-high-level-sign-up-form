# Task Completion

The assignment will be completed using _SOLID_ principles approach.

> Before getting acquainted with Task Completion documentation you may want to read why this approach was chosen. You can find approach documentation [here](../approach/index.md).

The main goal of choosing _SOLID_ principles approach is:

- If we need to make a change to `SignupForm`, then such a change should be made in a single place and preferably in such a way that will not change the code that already works. Instead we should be able to add new code that will change the component's behavior.
- It should be possible to create a new version of the component reusing already existing code.
- The risk that new changes will break something should be minimized.

## Components Documentation

This is a high-level documentation for `SignupForm` component. Full implementation can be found [here](https://github.com/NtonBala/sign-up-form-solid-react).

> [!IMPORTANT]
> Asterisk (**\***) is used to highlight a reusable component, e.g. SignupForm\*.

Components list with naming (real names):

- [SignupForm](#signupform)\*
  - [initialValues](#initialvalues)
  - [useFormStore](#useformstore-tinitialstate-formstatet--signupformstore)
  - [validate](#validate-values-signupformvalues--partialsignupformvalues)
  - [submit](#submit-username-string-password-string--promiseunknown)
  - [renderFormFields](#renderformfields-store-signupformstoresignupformvalues--jsxelement)
  - [renderSubmitButton](#rendersubmitbutton-store-signupformstoresignupformvalues--jsxelement)
- [TextInput](#textinput)\*
- [SubmitButton](#submitbutton)\*

### SignupForm\*

A **reusable component**, responsible for constructing a specialized version of native HTML form element. Reusability is achieved by reusing various parts of already existing code.

It implements _OCP_ principle: `SignupForm` should allow to replace all of its implementation details without touching its own code. This is achieved by passing things that `SignupForm` uses as well as its implementation details via props. Such approach makes `SignupForm` _extendable_: instead of changing its code, you can change its behavior by passing implementation details via its props:

- `initialValues` - defines form store shape
- `useFormStore` - a custom hook used to create form store (form state + state handlers)
- `validate` - is used to get `errors` object
- `submit` - to submit data to API endpoint
- `renderFormFields` - provides form fields UI
- `renderSubmitButton` - specifies how submit button is rendered

This component is also responsible for providing general layout. If you want to change general layout you should change this component.

#### initialValues

An object that is used as `FormState` generic type prop to define form store shape.

#### useFormStore: `<T>(initialState: FormState<T>) => SignupFormStore`

An optional custom generic react hook prop responsible to implement _SRP_ principle: to serve as a single place for creating, maintaining and holding form store logic.

It also implements _OCP_ principle: you may use it if you want to change how the store is updated, otherwise just pass `initialValues` prop.

#### validate: `(values: SignupFormValues) => Partial<SignupFormValues>`

An optional function prop responsible to implement _SRP_ principle: to serve as a single place for holding validation logic and creating a form errors object.

It also implements _OCP_ principle: use it when your initial values differ from default `initialValues` prop.

#### submit: `(formValues: SignupFormValues) => Promise<unknown>`

An optional function prop responsible to implement _SRP_ principle: to serve as a single place for calling an API endpoint and submitting form data.

It also implements _OCP_ principle: use it if you want other API calling behavior than default.

#### renderFormFields: `(store: SignupFormStore<SignupFormValues>) => JSX.Element`

An optional _render prop_ responsible to implement _OCP_ principle: if you want to change how form fields are rendered you can do it without modifying `SignupForm` component, just by passing this prop.

#### renderSubmitButton: `(store: SignupFormStore<SignupFormValues>) => JSX.Element`

An optional _render prop_ responsible to implement _OCP_ principle: if you want to change how _form submit button_ is rendered you can do it without modifying `SignupForm` component, just by passing this prop.

### TextInput\*

A _standalone_ _dumb_ **reusable component**, responsible to implement _SRP_ principle: to serve as a single place for holding render logic of _standalone text input_ field.

### SubmitButton\*

A _standalone_ _dumb_ **reusable component**, responsible to implement _SRP_ principle: to serve as a single place for holding _standalone submit button_ render logic.
