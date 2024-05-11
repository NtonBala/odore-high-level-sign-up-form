# Task Completion

Form instance is created combining state management reusable elements:

- Form
- FormField, component created by `formFieldFactory` factory method

with a set of reusable form components, like `<FormTemplate />` and `<TextField />` or `<SelectField />`.

Form implementation require next elements:

- form data model type
- FormField element prepared for form model
- initial values
- on submit callback
- Form component
- form skeleton

In order to create a form you need to wrap your controls by `<Form />` element which initializes a new instance of the form and provides the whole API for managing the values (including validation, submitting the changes, accessing all metadata etc).

The form mechanism is based on react context so elements are available inside the component body.

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
            <FormField valuePath="username">{(fieldRenderProps) => <TextField {...fieldRenderProps} />}</FormField>

            <FormField valuePath="password">{(fieldRenderProps) => <TextField type="password" {...fieldRenderProps} />}</FormField>
          </div>
        </FormTemplate>
      )}
    </Form>
  );
};
```

**_Validation_**

All elements presented above are inserted into one component only for presentation purpose. In real case it's better to follow SRP principle and move distinct units to dedicated files.

The following responsibilities can be identified:

1. Form skeleton (controls layout)
1. Data structure definition
1. Validation
1. Submitting action

So sign-up form feature structure with _username_, _password_ and _gender select_ can look like this:

```
ExtendedSignUpForm
├── commands
│   └── submitChanges.ts
├── validation
│   └── validate.ts
├── data.ts
└── ExtendedSignUpForm.tsx
```
