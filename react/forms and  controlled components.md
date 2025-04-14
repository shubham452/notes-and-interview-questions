**📝 Forms and Controlled Components in React**

**1. What is the difference between controlled and uncontrolled
components?**

  **Feature**             **Controlled Component**                                **Uncontrolled Component**
  ----------------------- ------------------------------------------------------- -----------------------------------------------------
  Data is stored in       React state                                             DOM (via refs)
  How value is accessed   value prop and onChange handler                         ref to access input value
  Ideal for               React-managed forms with validation and dynamic input   Simple forms or when integration with DOM is needed
  Example                 &lt;input value={state} onChange={handleChange} /&gt;   &lt;input ref={inputRef} /&gt;

**2. How do you handle form state in React?**

-   Use useState for each input or combine into a single object:

js

const \[formData, setFormData\] = useState({ name: "", email: "" });

const handleChange = (e) =&gt; {

setFormData({ ...formData, \[e.target.name\]: e.target.value });

};

-   Then bind it to inputs:

jsx

&lt;input name="name" value={formData.name} onChange={handleChange}
/&gt;

**3. What is Formik, and how does it help with form handling?**

-   **Formik** is a library for building forms in React:

    -   Manages form state and submission.

    -   Simplifies form validation.

    -   Reduces boilerplate code.

**Key Features:**

-   useFormik or &lt;Formik&gt; component

-   Built-in support for **Yup** validation

-   Field-level validation and error tracking

js

const formik = useFormik({

initialValues: { email: "" },

onSubmit: (values) =&gt; console.log(values),

});

**4. How do you validate forms in React?**

**🧼 Manual Validation**

-   Use if statements inside handleSubmit to check each field.

**✅ Using Formik + Yup**

js

const validationSchema = Yup.object({

email: Yup.string().email().required(),

});

**✅ Using custom logic**

-   Track errors in a state object and display conditionally.

**5. How can you handle file uploads in React?**

1.  Use an &lt;input type="file" /&gt; element.

2.  Use FormData to send files to backend.

js

const handleFileChange = (e) =&gt; {

const file = e.target.files\[0\];

const formData = new FormData();

formData.append("file", file);

fetch("/upload", {

method: "POST",

body: formData,

});

};

**1. Controlled vs. Uncontrolled Inputs**

**Controlled Inputs**

-   **Definition:** Components where form data is handled by
    React state. Every state mutation has an associated handler.

-   **Characteristics:**

    -   The input's value is set via the state.

    -   Changes made by the user are captured through events
        (e.g., onChange) that update the state.

-   **Benefits:**

    -   Easier to enforce validation, formatting, and
        conditional rendering.

    -   Single source of truth (React state).

-   **Example:**

> jsx
>
> import { useState } from 'react';
>
> function ControlledForm() {
>
> const \[name, setName\] = useState('');
>
> const handleChange = (e) =&gt; {
>
> setName(e.target.value);
>
> };
>
> return (
>
> &lt;div&gt;
>
> &lt;label htmlFor="name"&gt;Name:&lt;/label&gt;
>
> &lt;input
>
> id="name"
>
> type="text"
>
> value={name}
>
> onChange={handleChange}
>
> /&gt;
>
> &lt;/div&gt;
>
> );
>
> }

**Uncontrolled Inputs**

-   **Definition:** Components where form data is handled by the DOM
    itself rather than React state.

-   **Characteristics:**

    -   Use of refs (useRef) to get current values.

    -   Typically simpler for less complex forms that do not require
        real-time validation.

-   **Benefits:**

    -   Lower overhead when state synchronization isn’t necessary.

-   **Example:**

> jsx
>
> import { useRef } from 'react';
>
> function UncontrolledForm() {
>
> const inputRef = useRef();
>
> const handleSubmit = (e) =&gt; {
>
> e.preventDefault();
>
> console.log('Input value:', inputRef.current.value);
>
> };
>
> return (
>
> &lt;form onSubmit={handleSubmit}&gt;
>
> &lt;label htmlFor="name"&gt;Name:&lt;/label&gt;
>
> &lt;input id="name" type="text" ref={inputRef} /&gt;
>
> &lt;button type="submit"&gt;Submit&lt;/button&gt;
>
> &lt;/form&gt;
>
> );
>
> }

**2. Handling onChange and onSubmit**

**onChange**

-   **Role:**

    -   Captures every change in input, allowing real-time updates to
        the component state.

    -   Often used in controlled components.

-   **Example:**

> jsx
>
> const handleChange = (e) =&gt; {
>
> setValue(e.target.value);
>
> };
>
> &lt;input value={value} onChange={handleChange} /&gt;;

**onSubmit**

-   **Role:**

    -   Captures the form submit event.

    -   Typically used to prevent the default browser behavior and to
        trigger custom submit logic (e.g., sending data to an API).

-   **Example:**

> jsx
>
> const handleSubmit = (e) =&gt; {
>
> e.preventDefault();
>
> // Process form data
>
> };
>
> &lt;form onSubmit={handleSubmit}&gt;
>
> &lt;input value={value} onChange={handleChange} /&gt;
>
> &lt;button type="submit"&gt;Submit&lt;/button&gt;
>
> &lt;/form&gt;

**3. Using useRef for DOM Interaction**

-   **Purpose:**

    -   useRef is a hook that provides a way to access DOM nodes or
        persist values across re-renders.

    -   In forms, it's particularly useful for uncontrolled inputs or
        managing focus.

-   **Common Use-Cases:**

    -   Focusing an input element on mount.

    -   Fetching the current value of an input when not using
        controlled components.

-   **Example:**

> jsx
>
> import { useRef, useEffect } from 'react';
>
> function AutoFocusInput() {
>
> const inputRef = useRef(null);
>
> useEffect(() =&gt; {
>
> // Automatically focus on the input element when mounted
>
> inputRef.current.focus();
>
> }, \[\]);
>
> return &lt;input ref={inputRef} type="text" /&gt;;
>
> }

**4. Libraries for Forms and Validation**

**Formik**

-   **Features:**

    -   A powerful library that simplifies form state management.

    -   Built-in support for form validation and error handling.

-   **Usage:**

    -   Define initial values, validation schema, and form
        submission logic.

-   **Example:**

> jsx
>
> import { Formik, Form, Field, ErrorMessage } from 'formik';
>
> function BasicForm() {
>
> return (
>
> &lt;Formik
>
> initialValues={{ name: '' }}
>
> onSubmit={(values) =&gt; console.log(values)}
>
> &gt;
>
> {() =&gt; (
>
> &lt;Form&gt;
>
> &lt;Field name="name" /&gt;
>
> &lt;ErrorMessage name="name" component="div" /&gt;
>
> &lt;button type="submit"&gt;Submit&lt;/button&gt;
>
> &lt;/Form&gt;
>
> )}
>
> &lt;/Formik&gt;
>
> );
>
> }

**React Hook Form**

-   **Features:**

    -   Leverages uncontrolled components and refs for
        better performance.

    -   Minimal re-renders and easy to integrate with third-party
        UI libraries.

-   **Usage:**

    -   Register input fields and handle form submission with its
        simple API.

-   **Example:**

> jsx
>
> import { useForm } from 'react-hook-form';
>
> function HookForm() {
>
> const { register, handleSubmit } = useForm();
>
> const onSubmit = (data) =&gt; console.log(data);
>
> return (
>
> &lt;form onSubmit={handleSubmit(onSubmit)}&gt;
>
> &lt;input {...register('name')} /&gt;
>
> &lt;button type="submit"&gt;Submit&lt;/button&gt;
>
> &lt;/form&gt;
>
> );
>
> }

**Yup for Validation**

-   **Purpose:**

    -   A JavaScript schema builder for value parsing and validation.

    -   Commonly used with Formik and React Hook Form to define
        validation rules.

-   **Usage:**

    -   Create schemas to validate form fields.

-   **Example:**

> jsx
>
> import \* as Yup from 'yup';
>
> const validationSchema = Yup.object({
>
> name: Yup.string()
>
> .required('Name is required')
>
> .min(2, 'Too Short!'),
>
> });

-   **Integration with Formik:**

> jsx
>
> &lt;Formik
>
> initialValues={{ name: '' }}
>
> validationSchema={validationSchema}
>
> onSubmit={(values) =&gt; console.log(values)}
>
> &gt;
>
> {/\* ...form JSX \*/}
>
> &lt;/Formik&gt;
