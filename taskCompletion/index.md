# Task Completion

Form instance is constructed combining state management reusable elements (`<Form />`, `<FormField />` component created by `formFieldFactory` factory method) with a set of reusable form components (`<FormTemplate />`, `<TextField />` or `<SelectField />`).

Form implementation require next elements:

- form data model type
- FormField element prepared for form model
- initial values
- on submit callback
- Form component
- form skeleton

In order to create a form you need to wrap your controls by `<Form />` element which initializes a new instance of the form and provides the whole API for managing the values (including validation, submitting the changes, accessing all metadata etc).

The form mechanism is based on React context so elements are available inside the component body.

**Component tree via code sample**

SignUpForm component with only 2 fields, for _username_ and _password_ can look like this:

```tsx
interface SignUpFormData {
  username: string | undefined;
  password: string | undefined;
}

const FormField = formFieldFactory<SignUpFormData>();

export const SignUpForm = (): JSX.Element => {
  const initialValues: SignUpFormData = {
    username: undefined,
    password: undefined,
  };

  const save = (values: SignUpFormData) => {
    // do what you need with form data
  };

  return (
    <Form initialValues={initialValues} onSubmit={save}>
      {(formRenderProps) => (
        <FormTemplate onSave={formRenderProps.onSubmit}>
          <div>
            <FormField valuePath="username">{(fieldRenderProps) => <TextField {...fieldRenderProps.input} />}</FormField>

            <FormField valuePath="password">{(fieldRenderProps) => <TextField type="password" {...fieldRenderProps.input} />}</FormField>
          </div>
        </FormTemplate>
      )}
    </Form>
  );
};
```

All elements presented above are inserted into one component only for presentation purpose. In real case it's better to follow SRP principle and move distinct units to dedicated files.

The following responsibilities can be identified:

1. Form skeleton (controls layout)
1. Data structure definition
1. Validation
1. Submitting action

So sign-up form sub-feature (with _username_, _password_ and _gender select_) structure can look like this:

```
ExtendedSignUpForm
├── commands
│   └── submitChanges.ts
├── validate.ts
├── data.ts
└── ExtendedSignUpForm.tsx
```

## Components Documentation

> [!IMPORTANT]
> Asterisk is used to highlight a reusable component, e.g. Form\*.

- [SignUpForm / ExtendableSignUpForm](#signupform-or-extendablesignupform)
- [Form\*](#form)
- [FormField\*](#formfield)
- [FormTemplate\*](#formtemplate)
- [TextField\*](#textfield)
- [SelectField\*](#selectfield)

### SignUpForm or ExtendableSignUpForm

Feature dedicated components that constructs a custom form instance based on reusable elements.

### Form\*

Creates form store instance that holds state (values, metadata) and state management methods. API implementation is based on OCP and DIP principles - form works with abstractions and expects implementation details (like on submit or validation) via props.

Form store is preserved in React context so child components have access to it (e.g. `<FormField />`).

### FormField\*

This component should be created by `formFieldFactory` factory method hiding component creation details from the user.

The component is responsible for preparing controls data and passing it via render prop:

```ts
<FormField>{(fieldRenderProps) => <TextField {...fieldRenderProps.input} />}</FormField>
```

This component relies on form store and should be used inside `<Form />` store context provider.

### FormTemplate\*

Reusable component responsible for providing single form layout. Implements OCP and DIP principles - works with abstractions and expects implementation details (like form fields or action controls) via props. Provides default action controls (Save and Cancel).

### TextField\*

Wrapper component for input control (the control itself can be a native input or web component, or components library input component). Is responsible for rendering the UI.

### SelectField\*

Wrapper component for select control (the control itself can be a native select or web component, or components library select component). Is responsible for rendering the UI.
